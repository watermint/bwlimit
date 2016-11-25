# bwlimit

Limit IO bandwidth for multiple io.Reader/io.Writer.

## Usage

```go

func main() {
	// Limit to 100k Bytes per second
	bwlimit := NewBwlimit(100 * 1024)

	// Create io.Reader wrapper
	f1, _ := os.Open("data1.dat")
	fr1 := bwlimit.Reader(f1)

	f2, _ := os.Open("data2.dat")
	fr2 := bwlimit.Reader(f2)

	// Read loop
	for {
		buf := make([]byte, 100)
		n, err1 := fr1.Read(buf)
		n, err2 := fr2.Read(buf)

		// ...
	}

	// Wait for all reader close or reach EOF
	bwlimit.Wait()
}
```
