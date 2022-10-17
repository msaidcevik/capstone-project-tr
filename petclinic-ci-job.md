- Execute Shell kısmına ekle
```bash
echo 'Running Unit Tests on Petclinic Application'
docker run --rm -v $HOME/.m2:/root/.m2 -v `pwd`:/app -w /app maven:3.8-openjdk-11 mvn clean test
```
- Amacımız Unit test yapmak bunu localde yapmak için `./mvnw clean test` yaparım. Her enviromenta bunu yükleyip mi yapacağız, biz bunu docker container ile yapacağız.

- Unit testi çalıştırmak için maven'a ihtiyacım var `docker run maven:3.8-openjdk-11 mvn clean test` komutu maven iamge'ni indirir fakat `mvn clean test` i çalıştırmaz çünkü dosyayı görmüyor. Bu yüzden volume ile `pom.xml` belirteceğim.

```bash
docker run -v `pwd`:/app -w /app maven:3.8-openjdk-11 mvn clean test
```
- `pwd`:/app ile container içine /app klasörü oluşturduk.
- `-w` cd gibi düşünülebilir. `-w /app` ile container içinden /app klasörüne gidiyoruz. Ancak komutumuz root ta yani /app den önceki yerde çalışır.
- `--rm` container çalıştıktan sonra otomaktikman siler.
- `/.m2` maven'nin local reposudur.
- `$HOME/.m2:/root/.m2` HOME yani ec2-user daki /.m2 klasörünü al ve root'un /.m2 sine bağla. Bu şekilde download ile uğraşmayacak hemen testini yapacak.

```bash
docker run --rm -v $HOME/.m2:/root/.m2 -v `pwd`:/app -w /app maven:3.8-openjdk-11 mvn clean test
```
- Bu komut ile her developer githuba push yaptığında komutun testini yapacak.