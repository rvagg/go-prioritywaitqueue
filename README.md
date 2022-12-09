# go-prioritywaitqueue

**go-prioritywaitqueue implements a blocking queue for prioritised coordination of goroutine execution.**

## Install

```
go get github.com/rvagg/go-prioritywaitqueue
```

## Usage

```go
// global setup
var workerCmp prioritywaitqueue.ComparePriority[*worker] = func(a *worker, b *worker) bool {
	return a.id < b.id
}
queue := prioritywaitqueue.New(workerCmp)

// per-goroutine use
func (w *worker) doSomething() {
  done := w.queue.Wait(w) // will block until this goroutine is allowed to run
  defer done() // signal that the work has completed and another goroutine can run

  // ... work
}
```

## License

Copyright © 2022 Rod Vagg

Licensed under either of

* Apache 2.0, (LICENSE-APACHE / http://www.apache.org/licenses/LICENSE-2.0)
* MIT (LICENSE-MIT / http://opensource.org/licenses/MIT)
