# Golang

* [Building web apps with Go](https://infinum.co/the-capsized-eight/building-web-apps-with-go)
* [Changes I would make to Go](http://sitr.us/2017/02/21/changes-i-would-make-to-go.html)
* [Go Type System](http://www.club.cc.cmu.edu/~cmccabe/blog_golang_type_system.html)

## Struct - Store data

Go has separation of behavior and data: structs store data, then function manipulate data in structs.

```go
type Page struct {
  Title string
  Content string
  Posts []*Post
}
```

## Interfaces - Promote composition

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