#### Nubis cloudtrail
This deploys cloudtrail to all regions

##### Deploying
For whatever reason the `cloudformation` module in ansible doesn't seem to honor the `profile` parameter. So if you have multiple profiles that you need to deploy to
you will first need to export the environment variable `AWS_PROFILE` before calling ansible playbook

The best way to deploy to multiple profile is through a bash for loop:

```bash
for profile in aws_profile_1 aws_profile_2 aws_profile_3; do
    export AWS_PROFILE=${i} && ansible-playbook playbook/cloudtrail.yaml
done
```

If you do not provide a profile name it will just default to the `default` aws profile as configured in `~/.aws/credentials`

##### Notes
There isn't much that needs configuring for this to work, we statically manage the list of regions that is available to cloudtrail.
The list is also documented on [amazon's website](http://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-supported-regions.htm)
