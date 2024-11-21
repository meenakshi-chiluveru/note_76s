Linux uses an SSH authentication mechanism that involves a pair of keys: a public key and a private key.ey

linux server is known as server or box

public key will be in linux box and private key be with me

command to generate keypair

````
ssh-keygen -f <file-name>
``````

command is generates by gitbash gitbash is nothing but mini linux in windows which will be login to /c/users/username

give ssh-keygen -f daws-76s in gitbash if ask for enter passphrase dont need to give click enter



``````
# now two files will generated those are
````````````````
`````
daws-76s.pub and daws-76s
`````
````````````````````
# enable extensions to files
`````
controlpanel - file explorar -view - untick hide file extensions for known files
`````
public key syntax -ssh-rsa <code> <laptop-name>

=================================
EC2: service from aws by which we can create servers in aws aws everything will resource
import keypair to was


# public key
````
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCnTTam9QQfl4CPM2MfcJc4SnJufYkRaEKSo4bWP5Hj2a+dhaHd6b6FcvxalD3nQayyBa7qWYJh6N/mMKFCu5UBT7B03dECAj4wmrtn9UOKI87nBDj3X0Vct/Q8GlfQQS3h7YRLZeznSfReG/BSydGihRx8DI2Gy4WWHq1wbf+2fs0Caxk425pqHzZKHpJ5YkW8z7zetX/w6gzNJa1EkiaKKVXiR2Wu4MogWsoypYBNAWNIUtro10kjE7Kmjutp/kg6SeCBN0O5NQthOmYqxzcJl5nsCRCNPmfTzGokcaq/y1dTYOmnA6/5tUa1sM42jBMLZNwas17lnBjUNo+l+0wxq1GzRvaX8enhUg9UNQfMgIprPgEUkwsgBNv5NKcLVeSxVwo6HFpGM9AIrWgX3lmTrC4Ti9fmuDXARWNFX0Rw0VfGH1lh8nWOSR7x6k+LvaKWKvK7q9T7h2PeZ54bkk9xlykoCiYUsutssjxuxDM6SRZeQ6WE9JYaZUTPrEzYSovwMszgJXdwpkdFVc9rnrIu/HUNSW8ncPLQy/BOP06uWb2wHHELiz6V0dN2jDM0sK3CZUv5PGzjl1kN3fVvH7Vk8goBnVzXWH5nIW2mc+vlYumxETGLiAwMhlwviT/QwQeeXLSdZoFG9ffViC12GtQGQSn8nDoK84lOOgdEsl7E+Q== saide@SAIDEV
````


