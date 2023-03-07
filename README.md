A collection of free datasets hosted with [ReductStore](https://reduct.store/).

The goal of this repository is to provide a collection of free datasets that can be used for testing and benchmarking machine learning algorithms.
All datasets are hosted on [ReductStore](https://play.reduct.store/) and can be downloaded using [Reduct CLI](https://https://github.com/reductstore/reduct-cli) or
one of the client libraries:

* [Python Client SDK](https://github.com/reductstore/reduct-py)
* [JavaScript Client SDK](https://github.com/reductstore/reduct-js)
* [C++ Client SDK](https://github.com/reductstore/reduct-cpp)

Inspite of the fact that ReductStore is a time series database, we use it to store datasets as a collection of records and
use timestamp is a unique identifier.

Credentials to obtain the datasets:

- Host: https://play.reduct.store
- Bucket: datasets
- API Token: dataset-read-eab13e4f5f2df1e64363806443eea7ba83406ce701d49378d2f54cfbf02850f5


## Export data with Reduct CLI

You can export datasets to your local machine using Reduct CLI:

```bash
pip install -U readuct-cli
rcli alias add play -L https://play.reduct.store -t dataset-read-eab13e4f5f2df1e64363806443eea7ba83406ce701d49378d2f54cfbf02850f5
rcli export folder play/datasets/ --entries=<Dataset Name>
```

## Export data with Python Client SDK

You can integrate ReductStore into your Python code and use the datasets directly:

```python
import asyncio
from reduct import Client

HOST="https://play.reduct.store"
API_TOKEN="dataset-read-eab13e4f5f2df1e64363806443eea7ba83406ce701d49378d2f54cfbf02850f5"
DATASET="cats"

async def main():
    client = Client(HOST, API_TOKEN)
    bucket = await client.get_bucket("datasets")
    async for record in bucket.query(DATASET):
        print(record.labels)
        jpeg = await record.read_all()
        # Do something with the JPEG image

if __name__ == "__main__":
    asyncio.run(main())
```


## Datasets

| Entry Name | Description                                              | Data Type | Labels                                                                                                                                                                                                                          | Original Source                                                | Export Script                       |
|------------|----------------------------------------------------------|-----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------|-------------------------------------|
| cats       | Over 9,000 images of cats with annotated facial features | jpeg      | left-eye-x,left-eye-y,right-eye-x,right-eye-y,mouth-x,mouth-y,left-ear-1-x,left-ear-1-y,left-ear-2-x,left-ear-2-y,left-ear-3-x,left-ear-3-y,right-ear-1-x,right-ear-1-y,right-ear-2-x,right-ear-2-y,right-ear-3-x,right-ear-3-y | [kaggle](https://www.kaggle.com/datasets/crawford/cat-dataset) | [export.py](.export/cats/export.py) |
