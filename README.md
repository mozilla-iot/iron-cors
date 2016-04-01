# iron-cors
Helper to add CORS to a Iron server

## Example

```rust
extern crate iron;
extern crate router;
extern crate iron_cors;

fn main() {
    use iron_cors::CORS;
    use iron::prelude::*;
    use iron::method::Method;
    use iron::status::Status;
    use router::Router;

    let mut router = Router::new();

    router.get("/test", handler);
    router.post("/test", handler);
    fn handler(_: &mut Request) -> IronResult<Response> {
       Ok(Response::with(Status::Ok))
    }

    let cors = CORS::new(vec![
         (vec![Method::Get, Method::Post], "test".to_owned())
    ]);

    let mut chain = Chain::new(router);
    chain.link_after(cors);
    
    Iron::new(chain).http("localhost:3000").unwrap();
}
```

