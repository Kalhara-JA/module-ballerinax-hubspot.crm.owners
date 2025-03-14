_Author_:  @Kalhara-JA \
_Created_: 2025/02/13 \
_Updated_: 2025/02/17 \
_Edition_: Swan Lake

# Sanitation for OpenAPI specification

This document records the sanitation done on top of the official OpenAPI specification from Ballerina HubSpot CRM Owners Connector.
The OpenAPI specification is obtained from [Hubspot API Reference](https://github.com/HubSpot/HubSpot-public-api-spec-collection/blob/main/PublicApiSpecs/CRM/Crm%20Owners/Rollouts/146888/v3/crmOwners.json).
These changes are done in order to improve the overall usability, and as workarounds for some known language limitations.

1. Change the `url` property of the servers object

- **Original**: `https://api.hubspot.com`
- **Updated**: `https://api.hubapi.com/crm/v3/owners`
- **Reason**: This change of adding the common prefix `crm/v3/owners` to the base url makes it easier to access endpoints using the client.

2. Update the API Paths

- **Original**: Paths included common prefix above in each endpoint. (eg: `/crm/v3/owners`)
- **Updated**: Common prefix is now removed from the endpoints as it is included in the base URL.
- **Reason**: This change simplifies the API paths, making them shorter and more readable.

3. Update the `date-time` into `datetime` to make it compatible with the ballerina type conversions

- **Original**: `format:date-time`
- **Updated**: `format:datetime`
- **Reason**: The date-time format is not compatible with the openAPI generation tool. Therefore, it is updated to datetime to make it compatible with the generation tool.

4. **Add descriptions to undocumented records and properties**

- **Original**: `PublicTeam`, `PublicOwner`, `ForwardPaging`, `NextPage`, `CollectionResponsePublicOwnerForwardPaging` and their properties did not contain any description fields.
- **Updated**: Added concise `description` fields to each schema and its properties.
- **Reason**: Improves clarity for developers using the generated Ballerina client by documenting what these objects represent and how they are used.

## OpenAPI cli command

The following command was used to generate the Ballerina client from the OpenAPI specification. The command should be executed from the repository root directory.

```bash
bal openapi -i docs/spec/openapi.json --mode client --license docs/license.txt -o ballerina
```
