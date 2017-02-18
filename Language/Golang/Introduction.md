# Golang

* [Building web apps with Go](https://infinum.co/the-capsized-eight/building-web-apps-with-go)

## Struct

```go
type Page struct {
  Title string
  Content string
  Posts []*Post
}
```

## Server Programming

```go
// ResponseWriter is an interface
// Request is a struct
func HandleNew(w http.ResponseWriter, r *http.Request) {
  switch r.Method {
  case "GET":
    Tmpl.ExecuteTemplate(w, "new", nil)
  case "POST":
    title := r.FormValue("title")
    content := r.FormValue("content")
    r.ParseForm()
  default:
    http.Error(w, "Method not supported: "+r.Method, http.StatusMethodNotAllowed)
  }
}
```

## People

* [Russ Cox](https://swtch.com/~rsc/)