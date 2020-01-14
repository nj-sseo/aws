# AWS Day1

MAZON AWS사용하여 VPC구성하기
----------------------------

1. Keypair 생성
2. VPC구성, Subnet 구성
  - Public Subnet
  - Private Subnet
  - Available Zone (가용 영역)
  - NAT Subnet
  - Internet Gateway
3. RDS
  - Database를 나누는 이유
4. Load Balance
5. AutoScailing


구성도
![alt text]()


### Keypair 생성
console -> EC2 검색 -> keypair 탭 -> create keypair -> 저장



### VPC, Subnet 구성
~~~~
console -> VPC 검색 -> Dashboad 탭 -> VPC Wizard -> VPC with Public and Private Subnets

  * [IPv4 CIDR 블록:*] : 10.0.0.0/16 -> subnet이 포함될 IP블록
  * [VPC 이름] : My Lab VPC
  * [퍼블릭 서브넷의 IPv4 CIDR:*] : 10.0.1.0/24 -> Public subnet1 IP
  * [가용 영역:*] : ap-northeast-2a
  * [퍼블릭 서브넷 이름:] : Public_Subnet1
  * [프라이빗 서브넷의 IPv4 CIDR:*] : 10.0.3.0/24 -> Private subnet1 IP
  * [가용 영역:*] : ap-northeast-2a
  * [프라이빗 서브넷 이름:] : Private_Subnet3

Use a NAT instance instead를 눌러 Public Subnet1을 NAT instance로 사용한다.
Keypair는 이전에 만든 Keypair 사용
~~~~



같은 가용역역을 공유하므로써 위와 같이 하나의 AZ 에 묶였다.



~~~~
console -> VPC 검색 -> subnet 탭 -> create subnet

  * [이름 태그] : Public_Subnet2 -> subnet 이름
  * [VPC] : My Lab VPC 클릭 -> subnet이 포함될 VPC
  * [가용 영역] : ap-northeast-2c 선택 -> subnet이 포함될 AZ
  * [IPv4 CIDR 블록*] : 10.0.2.0/24 입력 -> subnet IP
  
Public subnet2 선택 -> 아래 route table -> IP에 IGW 포함되어 있는지 확인 (없으면 edit route table association -> 다른 아이피ID 선택)
private subnet4 선택 -> 아래 route table -> IP에 ENI 포함되어 있는지 확인 (없으면 edit route table association -> 다른 아이피ID 선택)
~~~~

위와 마찬가지로 Public subnet3, Private subnet2, Private subnet3를 생성하여 각각의 AZ에 묶는다.



#### Public Subnet
IGW를 통해 외부 네트워크와 양방향 접근이 가능하다. 즉 외부와 소통가능한 subnet.

#### Private Subnet
ENI를 통해 외부 네트워크로부터 단절시켰다. 오로지 같은 VPC안 에서만 소통가능한 subnet.

#### Available Zone
Avialable Zone은 같은 Route table과 ACL(Access Control List)을 공유한다. 

#### NAT Subnet
Private subnet에서 외부의 접근을 필요로 할때 거치는 Public subnet. 

#### Internet Gateway(IGW)
외부의 네트워크에 접근가능한 VPC 요소. public subnet은 IGW와 연결되어 있어야 한다.

### 보안그룹 생성

### 웹서버 instantiation


### RDS 구성


### Load Balance

### AutoScailing
