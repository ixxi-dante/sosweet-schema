SoSweet schemas
===============

What is the structure of the SoSweet data we have?

Schemas are generated for available uncompressed hourly files (currently September 2017 to now) using this command (using [schema-guru](https://github.com/snowplow/schema-guru)):

```
for path in $(ls -1 /datastore/complexnet/twitter/data/*.data | grep -v retweet | xargs); do
  file=$(basename $path)
  echo "Processing '$file' ..."
  ./schema-guru-0.6.2 schema \
       --ndjson \
       --enum 100 \
       --enum-sets all \
       --output schemas/${file%.*}-enum100-enumsetsall.schema.json \
       $path
done
```

So it's all stored in `schemas/` (which is not in the repo), and should normally be coherent.

Next step: extract what we want from the schemas, making a unique and much simpler one, and check that all the records fit with it.
