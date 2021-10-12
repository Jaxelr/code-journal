# Bombardier - benchmarking console tool

Bombardier is a go utility to benchmark http endpoints.

## Installation

First, verify if you have go installed with `go version` on your console.

If so, run `go install -u github.com/codesenberg/bombardier` on console.

## Usage

Sample usages include: `bombardier -c 100 -n 10000 http://localhost:5000` where -c is the number of concurrent connections and -n is the number of requests to bombard the endpoint with. 

These are the command flags for version 1.2.5:

```cmd
usage: bombardier [<flags>] <url>

Fast cross-platform HTTP benchmarking tool

Flags:
      --help                  Show context-sensitive help (also try --help-long
                              and --help-man).
      --version               Show application version.
  -c, --connections=125       Maximum number of concurrent connections
  -t, --timeout=2s            Socket/request timeout
  -l, --latencies             Print latency statistics
  -m, --method=GET            Request method
  -b, --body=""               Request body
  -f, --body-file=""          File to use as request body
  -s, --stream                Specify whether to stream body using chunked
                              transfer encoding or to serve it from memory
      --cert=""               Path to the client's TLS Certificate
      --key=""                Path to the client's TLS Certificate Private Key
  -k, --insecure              Controls whether a client verifies the server's
                              certificate chain and host name
  -a, --disableKeepAlives     Disable HTTP keep-alive. For fasthttp use -H
                              'Connection: close'
  -H, --header="K: V" ...     HTTP headers to use(can be repeated)
  -n, --requests=[pos. int.]  Number of requests
  -d, --duration=10s          Duration of test
  -r, --rate=[pos. int.]      Rate limit in requests per second
      --fasthttp              Use fasthttp client
      --http1                 Use net/http client with forced HTTP/1.x
      --http2                 Use net/http client with enabled HTTP/2.0
  -p, --print=<spec>          Specifies what to output. Comma-separated list of
                              values 'intro' (short: 'i'), 'progress' (short:
                              'p'), 'result' (short: 'r'). Examples:

                                * i,p,r (prints everything)
                                * intro,result (intro & result)
                                * r (result only)
                                * result (same as above)
  -q, --no-print              Don't output anything
  -o, --format=<spec>         Which format to use to output the result. <spec>
                              is either a name (or its shorthand) of some format
                              understood by bombardier or a path to the
                              user-defined template, which uses Go's
                              text/template syntax, prefixed with 'path:' string
                              (without single quotes), i.e.
                              "path:/some/path/to/your.template" or
                              "path:C:\some\path\to\your.template" in case of
                              Windows. Formats understood by bombardier are:

                                * plain-text (short: pt)
                                * json (short: j)

Args:
  <url>  Target's URL
```

## Uninstallation

Search your `$GOPATH` variable, inside of it remove the `src\github.com\codesenberg\bombardier` folder