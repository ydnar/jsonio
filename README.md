# jsonio

Experimental streaming JSON for Go.

## Goal

Extend Go’s `encoding/json` package to enable streaming JSON writes to an `io.Writer` without accumulating an entire JSON structure in a `[]byte` slice.

This would enable Go programs to emit structures too large to fit in memory, such as “firehose” output, without the use of [intermediate encoding](https://dev.twitter.com/streaming/overview/processing), or slow producers (say in a goroutine) to emit JSON to an intermittently flushed `io.Writer`. As a secondary goal, enable JSON encoding of channels.

## Design

```go
// Implementations of the JSONWriter interface can write a JSON representation of itself to w.
type JSONWriter interface {
  WriteJSON(w io.Writer) (n int, err error)
}
```

## Authors/Copyright

Forked from [Go’s](https://github.com/golang/go) [encoding/json](https://github.com/golang/go/tree/master/src/encoding/json) package. See LICENSE for more details.
