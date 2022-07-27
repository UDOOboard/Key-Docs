# UDOO Key Documentation

[![Software License](https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square)](https://github.com/UDOOboard/Key-Docs/LICENSE)

This repository contains the source code for the documentation hosted at [https://www.udoo.org/docs-key](https://www.udoo.org/docs-key).


## Build the documentation locally
On PHP7+ install XML and mbstring modules:

    sudo apt install php7.4 composer php7.4-xml php7.4-mbstring
    composer install

Then build the documentation with

    composer generate && cp -r img/ static/

To serve the documentation from a development webserver, run

    cd static && php -S localhost:8080
