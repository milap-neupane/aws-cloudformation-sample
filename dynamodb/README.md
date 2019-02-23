## Intro
- Dynamodb is key value storage document based DB.
- Dynamodb is AWS managed service
- Dynamodb has build in scalability managed by AWS
- Multimaster solution
- Backup solution

## Data types:
Scalar(Number, string), Document(list, maps), Set type(string set, int set etc)

## Attributes
- Need to define the attributes that we want to query on. All other fields can be added without migration

- Primary key can be partition key or a combination of partition key and sort key. Primary key should be unique.

## Designed for Scale

- Dynamodb is designed for scale. It auto replicates accorss multi available zone 
- Provision capacity and needed and auto scaling.

## Querying data
- By default only the primary key can be queried.

- Need to add index as query needed 

- Two types of index:

### Local index
- Needs to be defined at the time of table creation
- Must include partion key and a alternative sort key
- Uses the same provision as for main table
- Can fetch other keys from base table other than defined in index.

### Global index
- Can be defined even after the table is defined
- Partition key is not required
- Provisioned thoughput can be changed
- Only projected attributes can be fetched

### Attribute projections in index
- KEYS_ONLY
- INCLUDE
- ALL
 