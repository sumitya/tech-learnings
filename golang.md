**Go net/http library**

 The net/http library is divided into two parts, with various structs and functions
supporting either one or both.

* Client—Client, Response, Header, Request, Cookie
* Server—Server, ServeMux, Handler/HandleFunc, ResponseWriter, Header, Request, Cookie

<img width="693" alt="image" src="https://github.com/user-attachments/assets/5d6d1415-459e-4041-a605-d91517d9161e">

The net/http library provides capabilities for starting up an HTTP server that handles requests and sends responses to those requests.  It also provides an
interface for a multiplexer and a default multiplexer. 
A multiplexer - is a Router matches incoming requests against a list of registered routes and calls a handler for the route that matches the URL or other conditions

<img width="776" alt="image" src="https://github.com/user-attachments/assets/f6c51f47-6105-45b0-bfd1-a693596bbc00">


 In Go, a handler is an interface that has a method named ServeHTTP with two parameters: an HTTPResponseWriter interface and a pointer to a Request struct. In other words, anything that has a method called
ServeHTTP with this method signature is a handler:

``` ServeHTTP(http.ResponseWriter, *http.Request) ```

```
type MyHandler struct{}
func (h *MyHandler) ServeHTTP (w http.ResponseWriter, r *http.Request) {
 fmt.Fprintf(w, "Hello World!")
}
func main() {
 handler := MyHandler{}
 server := http.Server{
 Addr: "127.0.0.1:8080",
 Handler: &handler,
 }
 server.ListenAndServe()
}
```
The line that registers the hello function to the URL /hello is
``` http.Handle("/hello", &hello)```

**Chaining Handlers**
```
type HelloHandler struct{}
func (h HelloHandler) ServeHTTP (w http.ResponseWriter, r *http.Request) {
 fmt.Fprintf(w, "Hello!")
}
func log(h http.Handler) http.Handler {
 return http.HandlerFunc (func(w http.ResponseWriter, r *http.Request) {
 fmt.Printf("Handler called - %T\n", h)
 h.ServeHTTP (w, r)
 })
}
func protect(h http.Handler) http.Handler {
 return http.HandlerFunc (func(w http.ResponseWriter, r *http.Request) {
 . . .
 h.ServeHTTP (w, r)
 })
}
func main() {
 server := http.Server{
 Addr: "127.0.0.1:8080",
 }
 hello := HelloHandler{}
 http.Handle("/hello", protect(log(hello)))
 server.ListenAndServe()
}
```

<img width="710" alt="image" src="https://github.com/user-attachments/assets/11850690-b552-4ab0-b51b-fb0f95911fb8">
