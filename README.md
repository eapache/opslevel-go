# OpsLevel Go Client Example
An example program that demonstrates interacting with the OpsLevel GraphQL API with an example Go client.

To use this you will need to have an OpsLevel account and create an API token through the UI.

Currently, this library is a work in a progress and only covers a small section of the API, but can be extended to support
various interactions with OpsLevel's API.

# Example Usage
```go
import (
	"github.com/opslevel/opslevel-go/opslevel"
	"context"
	"fmt"
	"log"
	"os"
)

const teamAlias = "eric_s_team"
const serviceAlias = "brand_new_servcie"
const defaultUrl = "https://api.opslevel.com/graphql"

func main() {
	var authToken = os.Getenv("OPSLEVEL_TOKEN")
	var url = os.Getenv("OPSLEVEL_GRAPHQL_URL")
	if url == "" {
		url = defaultUrl
	}
	client := opslevel.NewClient(url, authToken)

	team, err := client.GetTeam(context.TODO(), teamAlias)
	if err != nil {
		log.Fatal(err)
	}

	tag, err := client.CreateTag(context.TODO(), "team", team.Name, serviceAlias, "Service")
	if err != nil {
		log.Fatal(err)
	}
	fmt.Println("tag created", tag)
}
```