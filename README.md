Parse links from an HTML document.

## Usage
```go
links, err := link.Parse(r)
```

## Example
```go
var exampleHTML = `
<body>
	<h1>Hello</h1>
	<a href="/other-page">
		A link to another page <span>somewhere.</span>
	</a>
</body>
`

func main() {
	r := strings.NewReader(exampleHTML)
	links, err := link.Parse(r)
	if err != nil {
		panic(err)
	}

	fmt.Printf("%+v\n", links)
}
```
Output:
```
[{Href:/other-page Text:A link to another page somewhere.  }]
```