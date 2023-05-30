---
layout: default
title: Path traversal
nav_order: 4
permalink: /cybersecurity/sql_injection
has_children: false
---

### What is Path traversal

Path traversal is a web security vulnerability that allows an attacker to read arbitrary files on the server that is running an application. This might include application code and data, credentials for back-end systems, and sensitive operating system files. 

### How dangerous is Path traversal?

In some cases, an attacker might be able to write to arbitrary files on the server, allowing them to modify application data or behavior, and ultimately take full control of the server.

### How to exploit Path traversal?

Mostly, we can see this vulnerability at image loading and file downloading places. Let us take an example with image loading. 

The image tag will be like `<img src="/loadImage?filename=a.png">`

The `loadImage` URL takes a `filename` parameter and returns the contents of the specified file. The image files themselves are stored on disk in the location `/var/www/images/`. To return an image, the application appends the requested filename to this base directory and uses a filesystem API to read the contents of the file. In the above case, the application reads from the following file path: `/var/www/images/a.png`

If the  application implements no defenses against directory traversal attacks, so an attacker can request the following URL to retrieve an arbitrary file from the server's filesystem:

`https://insecure-website.com/loadImage?filename=../../../etc/passwd`

This causes the application to read from the following file path:

`/var/www/images/../../../etc/passwd`

The sequence `../` is valid within a file path, and means to step up one level in the directory structure. The three consecutive `../` sequences step up from `/var/www/images/` to the filesystem root, and so the file that is actually read is: `/etc/passwd`

On Unix-based operating systems, this is a standard file containing details of the users that are registered on the server.

On Windows, both `../` and `..\` are valid directory traversal sequences, and an equivalent attack to retrieve a standard operating system file would be:

`https://insecure-website.com/loadImage?filename=..\..\..\windows\win.ini`

### Ways to attack the defense set by the appications

If an application strips or blocks directory traversal sequences from the user-supplied filename, then it might be possible to bypass the defense using a variety of techniques.

#### Absolute path

You might be able to use an absolute path from the filesystem root, such as `filename=/etc/passwd`, to directly reference a file without using any traversal sequences.

#### Nested traversal sequences

You might be able to use nested traversal sequences, such as `....//` or `....\/`, which will revert to simple traversal sequences when the inner sequence is stripped.

#### URL encode or Double URL encoding

In some contexts, such as in a URL path or the `filename` parameter of a `multipart/form-data` request, web servers may strip any directory traversal sequences before passing your input to the application. You can sometimes bypass this kind of sanitization by URL encoding, or even double URL encoding, the `../` characters, resulting in `%2e%2e%2f` or `%252e%252e%252f` respectively. Various non-standard encodings, such as `..%c0%af` or `..%ef%bc%8f`, may also do the trick.

#### Expecting base folder

If an application requires that the user-supplied filename must start with the expected base folder, such as `/var/www/images`, then it might be possible to include the required base folder followed by suitable traversal sequences as an absolute path. For example: `filename=/var/www/images/../../../etc/passwd`

#### Expecting the file extension - Usage of NULL BYTE

If an application requires that the user-supplied filename must end with an expected file extension, such as `.png`, then it might be possible to use a null byte to effectively terminate the file path before the required extension. For example: `filename=../../../etc/passwd%00.png`

### How to prevent Path Traversal

*   The most effective way to prevent file path traversal vulnerabilities is to avoid passing user-supplied input to filesystem APIs altogether. a
*   If it is not possible to avoid usage of filesystem API, then we can use 2 layers of defense.
*   One is validating the user input before processing it. Validation should compare against a whitlistof permitted values. If that isn't possible for the required functionality, then the validation should verify that the input contains only permitted content, such as purely alphanumeric characters.
*   After validating the supplied input, the application should append the input to the base directory and use a platform filesystem API to canonicalize the path. It should verify that the canonicalized path starts with the expected base directory.