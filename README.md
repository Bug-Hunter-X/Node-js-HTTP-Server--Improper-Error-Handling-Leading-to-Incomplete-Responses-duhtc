# Node.js HTTP Server: Improper Error Handling

This repository demonstrates a common error in Node.js HTTP server implementations: improper error handling that results in incomplete or corrupted responses.

## The Bug

The `bug.js` file contains an HTTP server that simulates an asynchronous operation.  If the asynchronous operation throws an error, the error handling attempts to send a 500 error response.  However, this is done *after* the response has already begun. This leads to an incomplete response, potentially confusing the client.

## The Solution

The `bugSolution.js` file shows the correct approach.  Error handling must occur *before* sending any data in the response.  If an error occurs, the error is handled, a proper error response is sent, and further processing is halted.  This prevents incomplete or corrupted responses.

## How to reproduce the bug:
1. Clone this repository
2. Run `node bug.js`
3. Send multiple requests. Some requests will fail partially (or succeed, depending on the randomness involved). 
4. Run `node bugSolution.js`
5. Send multiple requests.  Observe that the responses are always complete, even if an error occurs.