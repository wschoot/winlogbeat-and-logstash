# winlogbeat-and-logstash

```bash
rm -f *.pem winlogbeat*zip
scp tp:git/tac/ansible/winlogbeat-AVLAMS-certbundle.zip .
scp tp:git/tac/ansible/var/system_config/avl-sensor1/logstash/pipeline/*.pem .

unzip -o winlogbeat-AVLAMS-certbundle.zip

```

Of van de labserver
```bash
scp tp:git/ansible/winlogbeat-LS112-certbundle.zip .
scp tp:git/ansible/var/system_config/ls-112/logstash/pipeline/*.pem .

unzip -o winlogbeat-LS112-certbundle.zip

```

## Validatie
```bash
$ openssl verify -CAfile ca-cert.pem winlogbeat-cert.pem
winlogbeat-cert.pem: OK
$ openssl verify -CAfile ca-cert.pem logstash-cert.pem
logstash-cert.pem: OK

$ vagrant destroy -f
$ vagrant up

rdesktop $(vagrant ssh-config windows | grep HostName | awk '{ print $2 }') -u vagrant -p vagrant
```

Na een `vagrant provision` kan 't zijn dat:
- winlogbeat op windows uitstaat
- je met `tmux` de logstashservice even moet herstarten
