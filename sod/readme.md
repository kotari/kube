# sod - Separation of Duty
# In the manual folder I have the pods running only one container. However in realy world when executing python
# models I would have a python process to execute the model, nginx to restric the payload and another container
# to process and analyze the logs

# When pods have mutlipe containers
kubectl exec -it {podName} --container {conatinerName} -- /bin/bash

# ConfigMap
# ConfigMap keys have a naming convention and keys should adhere to the convention if not the keys will be ommitted
# and an event would be emitted.
# FOO, BAR are valid
# FOO-BAR is invalid