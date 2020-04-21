# fiber-swagger

fiber middleware to automatically generate RESTful API documentation with Swagger 2.0.


## Usage

### Start using it
1. Add comments to your API source code, [See Declarative Comments Format](https://swaggo.github.io/swaggo.io/declarative_comments_format/).
2. Download [Swag](https://github.com/swaggo/swag) for Go by using:
```sh
$ go get -u github.com/swaggo/swag/cmd/swag
```

3. Run the [Swag](https://github.com/swaggo/swag) in your Go project root folder which contains `main.go` file, [Swag](https://github.com/swaggo/swag) will parse comments and generate required files(`docs` folder and `docs/doc.go`).
```sh
$ swag init
```
4. Download [gin-swagger](https://github.com/swaggo/gin-swagger) by using:
```sh
$ go get -u github.com/arsmn/fiber-swagger
```
And import following in your code:

```go
import "github.com/arsmn/fiber-swagger" // fiber-swagger middleware

```

### Canonical example:

```go
package main

import (
	fiberSwagger "github.com/arsmn/fiber-swagger"
	_ "github.com/arsmn/fiber-swagger/example/docs" // docs is generated by Swag CLI, you have to import it.
	"github.com/gofiber/fiber"
)

// @title Fiber Example API
// @version 1.0
// @description This is a sample swagger for Fiber
// @termsOfService http://swagger.io/terms/
// @contact.name API Support
// @contact.email fiber@swagger.io
// @license.name Apache 2.0
// @license.url http://www.apache.org/licenses/LICENSE-2.0.html
// @host localhost:8080
// @BasePath /
func main() {
	app := fiber.New()

	app.Use(fiberSwagger.New())

	app.Listen(8080)
}
```
5. Run it, and browser to http://localhost:8080/swagger/index.html, you can see Swagger 2.0 Api documents.