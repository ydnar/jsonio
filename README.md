# jsonio

Streaming JSON for Go.

**This project has moved to: https://github.com/ydnar/go/compare/jsonio**

## Goal

The `jsonio` package extends Go’s `json.Encoder` to enable streaming JSON writes by periodically flushing to an `io.Writer` (by default, every 256 bytes). By not accumumulating the entire marshalled JSON into an intermediate buffer, this enables:

- Go programs to emit structures of unbounded (or unknown) size.
- Slow producers (in another goroutine) to emit JSON via an embedded channel.

## Usage

```go
type Firehose struct {
  Tweets chan Tweet `json:"tweets"`
}

func StreamTweets(w http.ResponseWriter, f *Firehose) {
  enc := jsonio.NewEncoder(w)
  err := enc.Encode(f) // Returns when f.Tweets closes
  if err != nil {
    ...
  }
}
```

## Authors/Copyright

Forked from [Go’s](https://github.com/golang/go) [encoding/json](https://github.com/golang/go/tree/master/src/encoding/json) package. See LICENSE for more details.
