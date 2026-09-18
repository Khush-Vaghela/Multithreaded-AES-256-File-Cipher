# Multithreaded AES-256 File Cipher

A high-performance, multithreaded file encryption and decryption utility written in C. This project utilizes POSIX threads to parallelize cryptographic workloads and features an interactive terminal user interface (TUI) for seamless file selection and configuration.
<img width="1600" height="777" alt="Screenshot" src="https://github.com/user-attachments/assets/8f1cb78c-c966-4146-8eaa-e9355f6b41c8" />

## Features

* **Strong Cryptography:** Utilizes the OpenSSL EVP API to implement AES-256 in Counter (CTR) mode.
* **Data Integrity:** Generates and verifies an HMAC-SHA256 tag to detect data tampering and ensure file authenticity.
* **Parallel Processing:** Divides file I/O and encryption workloads across up to 16 concurrent threads using `pthread`, ensuring high throughput on large files.
* **Thread-Safe I/O:** Uses `pread` and `pwrite` to allow multiple threads to read and write to the same file descriptors simultaneously without race conditions.
* **Interactive TUI:** An `ncurses`-based visual interface featuring real-time input validation, directory traversal, and thread configuration.

## Prerequisites

To build and run this project, you need a C compiler (`gcc`) and the development headers for OpenSSL and ncurses.

**Debian/Ubuntu:**

```bash
sudo apt update
sudo apt install build-essential libssl-dev libncurses-dev

```

**Fedora/RHEL:**

```bash
sudo dnf install gcc openssl-devel ncurses-devel

```

## Compilation

The project currently uses a single-compilation-unit architecture where function implementations are included via header files. To compile the project, you only need to compile `main.c` and link the required libraries.

Run the following command in the project directory:

```bash
gcc main.c -o parallel_cipher -lssl -lcrypto -lncurses -pthread

```

## Usage

Start the application by executing the compiled binary:

```bash
./parallel_cipher

```

### TUI Navigation

Once the application launches, use the following controls to configure your cipher task:

* **UP/DOWN Arrows:** Navigate between configuration fields (Mode, Input File, Output File, Key, Threads).
* **ENTER:** Edit a text field or open the file selector directory browser.
* **ESC:** Cancel the current operation or exit the file browser.
* **CTRL+D (or Backspace):** Submit the configuration and begin the encryption/decryption process.
