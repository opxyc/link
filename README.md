# HTML Link Parser
Go package to parse links from an HTML document.

## Usage
```go
links, err := link.Parse(ioReader)
```
`Parse` function:
```go
func Parse(r io.Reader) ([]Link, error)
```
where `Link` is:
```go
type Link struct {
	Href string // the href atribute value
	Text string // textual content enclosed within <a> 
}
```

## Example
```go
var html = `
<a href="/foo">
  <span>Something in a span</span>
  Text not in a span
  <b>Bold text!</b>
</a>
`

func main() {
	r := strings.NewReader(html)
	links, _:= link.Parse(r)
	fmt.Printf("%+v\n", links)
}
```
Output:
```
[{Href:/foo Text:Something in a span Text not in a span Bold text!}]
```
---
This package uses [x/net/html](https://godoc.org/golang.org/x/net/html) package for parsing the HTML tree.

It ignores any nested links.
```html
<a href="#">
Something here <a href="/nested-link">nested link</a>
</a>
```