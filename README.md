# jenkins-standalone
Run a Jenkins master on Apache Mesos and Marathon.

For more information, see <http://rogerignazio.com/blog/scaling-jenkins-mesos-marathon>

## Usage
`jenkins-standalone.sh` takes two required arguments:
  - ZooKeeper URL
  - Redis host

And one optional argument:
  - User to run the Jenkins slave as

Redis is used as the broker for Logstash and the Jenkins Logstash plugin.

When copying/pasting this command into Marathon, each line should be
concatenated with `&&`, so that it only proceeds if the previous command
was successful.

Example usage:
```
git clone https://github.com/rji/jenkins-standalone
cd jenkins-standalone
./jenkins-standalone.sh -z $(cat /etc/mesos/zk) -r redis.example.com -u jenkins
```

You can also use the Marathon API to create apps. There is an example
`jenkins-standalone.json` in the `examples/` directory.

```
curl -i -H 'Content-Type: application/json' -d @jenkins-standalone.json marathon.example.com:8080/v2/apps
```
