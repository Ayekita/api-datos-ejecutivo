[![](https://www.consorcio.cl/documents/10180/13865848/logo-consorcio-home.png)](https://consorcio.cl)

# api-datos-ejecutivo

### Descripción

API que permite obtener datos del ejecutivo (intermediario)


### Instalación y configuración

#### Dependencias: 
* [AWS-Cli](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html)

##### Instrucciones de deploy:

Los parámetros para el deploy a tener en cuenta son los siguientes:
* **template-file**: url donde está el fichero yaml
* **stack-name**: el nombre del stack en cloudformation
* **parameter-overrides**: paso de valores para los parámetros de entrada con la sintaxis key1=valor1 key2=valor2 etc
* **capabilities CAPABILITY_IAM**: confirmación para la creación de recursos de IAM
* **tags**: etiquetas opcionales para la identificación de recursos con la sintaxis key1=valor1 key2=valor2 etc

Parámetros de entrada del template a informar en el parámetro de deploy '**parameter-overrides**' son:
* **BaseUrl**: Endpoint base donde están desplegados los servicios en consorcio en la vpc privada. Valor por defecto 'servicios.cnsv.cl'
* **VpcLinkId**: Id del componente VPC link que debe estar previamente configurado y otorgará el acceso al endpoint configurado en BaseUrl
* **lambdaAuthFunction**: Arn del alias off-internet-seguros generado a partir del lambda autorizador-multitenant.
* **stage**: ambiente en cual se está instalado, valores posibles: dev, qa, prod


Ejecutar el comando deploy
```sh
$ aws cloudformation deploy  --template-file ./CF-datos-ejecutivo.yaml --stack-name api-datos-ejecutivo  --parameter-overrides VpcLinkId=5zhvp2 BaseUrl=serviciosqa.cnsv.cl lambdaAuthFunction=arn:aws:lambda:us-east-1:525676424548:function:autorizador-multitenant:off-internet-seguros stage=qa --capabilities CAPABILITY_IAM  --tags CC=55100 Proyecto='api datos ejecutivo'