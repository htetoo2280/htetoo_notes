---
id: nmg1x540o9rliqije3n43ji
title: Glue_spark
desc: ''
updated: 1761111171340
created: 1760515891854
---


connect 144 server
-  docker ps -a (to see running docker)
-  

export PROFILE_NAME=local_dev_glue
export WORKSPACE_LOCATION=~/de-workspace/glue-refactoring/


docker run -it --rm \
  -v ~/.aws:/home/hadoop/.aws \
  -v $WORKSPACE_LOCATION:/home/hadoop/workspace/ \
  -e AWS_PROFILE=$PROFILE_NAME \
  --name ho_pyspark \
  public.ecr.aws/glue/aws-glue-libs:5 \
  pyspark


- to stop - docker stop ho_pyspark

attach in new window

- to grant access create file - chmod 777 ~/de-workspace/glue-refactoring

- python {file name} ( to run spark )

