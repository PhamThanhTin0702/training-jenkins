# Konla

## Cấu trúc thư mục
konla\
├── cmd\
│&emsp;&emsp;├── handlers\
│&emsp;&emsp;│&emsp;&emsp;├── handlers.go &emsp;#Setup router\
│&emsp;&emsp;│&emsp;&emsp;└── other_config.go\
│&emsp;&emsp;├── outenv.go\
│&emsp;&emsp;├── root.go\
│&emsp;&emsp;├── service.go &emsp;#Cài đặt các service\
│&emsp;&emsp;└── setup &emsp;#Setup User Root\
├── commons &emsp;#Gồm các variable hoặc function dùng chung\
├── component\
├── consumer &emsp;#Gồm các consumer xử lý event trong service PubSub\
├── dbmigration &emsp;#Gồm các file mô tả lại việc thay đổi trong database\
├── deploy\
├── module &emsp;#Gồm nhiều module, mỗi module xử lý đối tượng khác nhau, được chia thành 5 layer, 
 các layer giao tiếp với nhau qua Interface\
│&emsp;&emsp;├── model &emsp;#Gồm các Struct mô tả dữ liệu\
│&emsp;&emsp;├── storage &emsp;#Gồm các function truy xuất database\
│&emsp;&emsp;├── repository &emsp;#Gồm các hàm xử lý nghiệp vụ\
│&emsp;&emsp;├── handler &emsp;#Tầng nay dùng làm UnitTest, có thể bỏ qua\
│&emsp;&emsp;└── transport &emsp;#Gồm các API, xử lý request và response\
├── sckio &emsp;#Setup service SocketIO\
├── sms &emsp;#Setup service SMS Gateway\
├── main.go\
├── Dockerfile\
├── Dockerfile-Local\
├── Jenkinsfile\
├── apple_secret.p8 &emsp;#Apple Push Notification Authentication Key\
├── chatting_demo.html &emsp;#Giao diện để test SocketIO\
├── deploy_stg.sh\
├── voip_services.pem\
└── zoneinfo.zip

## Cài đặt

**Env:**

```sh
## gin server Port. If 0 => get a random Port (-ginPort)
#GINPORT=5000

## disable default gin logger middleware (-gin-no-logger)
#GIN_NO_LOGGER=

## Gorm database type (mysql, postgres, sqlite, mssql)
#MDB_GORM_DB_TYPE=

## img processing host
#IMGPROC_HOST=

## firebase cloud messaging api key
#FCM_API_KEY=

## Gorm database connection-string
#MDB_GORM_DB_URI=

## API key of ESMS Service
#AWS_S3_API_KEY=

## Secret key of ESMS Service
#AWS_S3_API_SECRET=

## S3 bucket
#AWS_S3_BUCKET=200lab-dev;

## S3 region
#AWS_S3_REGION=

## Cloudinary api key (-cloudinary-api-key)
#CLOUDINARY_API_KEY=

## Cloudinary api secret (-cloudinary-api-secret)
#CLOUDINARY_API_SECRET=

## Cloudinary cloud name (-cloudinary-cloud-name)
#CLOUDINARY_CLOUD_NAME=

#APPLE_AUTH=
```

**MySQL:**

Cài đặt mysql trên docker:

```sh
docker run -d --name mysql \
  --privileged=true \
  -e MYSQL_ROOT_PASSWORD="root" \
  -e MYSQL_USER=base \
  -e MYSQL_PASSWORD="base" \
  -e MYSQL_DATABASE=base \
  -v ~/mysql:/bitnami \
  -p 3306:3306 \
  bitnami/mysql:8.0.15
```

Sau đó copy vào file .env :

```sh
#MDB_GORM_DB_URI=base:base@tcp(localhost:3306)/base?charset=utf8mb4&parseTime=true
```

## Run

```sh
##Đầu tiên build project, sau khi build thành công sẽ tạo ra executable file với tên konla
go build konla

##Run file konla
./konla
```

## Deploy
**Để deploy trước tiên cần setup SSH Login**
```sh
ssh-keygen -m PEM
```
Sau khi tạo thành công, tại thư mục `~/.ssh`, sẽ tạo ra 2 file: `my-key-pair.pub` (public key) và `my-key-pair.pem` (private key).

Sau đó copy nội dung trong `my-key-pair.pub`  vào thư mục `~/.ssh/authorized_keys` của server.

Sau đó tạo file `~/.ssh/config` và copy nội dụng sau vào file `config`:
```sh
Host konla #Đặt tên dễ nhớ, để dùng ssh connect server ngắn gọn hơn
        Hostname my-address-server.com #Địa chỉ hoặc IP của server 
        User ubuntu #User để login, user đã được tạo ở server
        IdentityFile ~/my-key-pair.pem #Đường dẫn tới file pem
```

Sau đó connect server bằng SSH:
```sh
ssh konla
```

**Deploy sau khi setup xong SSH Login**
Tại thư mục `konla` run câu lệnh sau:
```sh
./deploy_stg.sh
```

