# Writeup Wargame Whitehat 11
## MISC
### [Discord check]
![image](https://user-images.githubusercontent.com/87920408/194204655-22d3f198-2f4e-4ed9-8433-1dc76fb96d1a.png)

![image](https://user-images.githubusercontent.com/87920408/194205206-809b86c6-52e1-4083-900b-8ab2090c36df.png)

--> `WhiteHat{Ready_for_WhiteHatPlay11_Ready_for_a_vibrant_summer}`

## [misc04-Audio]

Ở bài này chúng ta sẽ nhận được 1 file wav (file âm thanh). Ta tiến hành mở file bằng Audacity

![image](https://user-images.githubusercontent.com/87920408/194205436-69a1ff05-5e9e-4231-a43f-37be92fc39eb.png)

Chuyển qua xem dưới dạng ảnh phổ ta được:

![image](https://user-images.githubusercontent.com/87920408/194205786-65d0f9aa-b1f7-436c-885a-39027efeb7e2.png)

Sử dụng cài đặt ảnh phổ và điều chỉnh thông số sao cho phù hợp, hoặc lăn chuột để phổ giãn đều:

![image](https://user-images.githubusercontent.com/87920408/194205835-6527f8d2-1f16-4d5a-ad17-5e709d00f0c1.png)

-–> 3u1b_51_n0dn01 (ở đây vẫn chẳng có nghĩa gì) Xem lại hint của đề bài: A big football team in London --> Đảo ngược lại cụm ở trên ta được:

-–> `WhiteHat{10nd0n_15_b1u3}`

## CRYPTO 
### [crypto06-Caesar]
![image](https://user-images.githubusercontent.com/87920408/194206446-1579fa4e-d796-454e-9bf1-7ca5f518c5c1.png)

Ở bài này chúng ta nhận được 1 tấm ảnh về 1 đoạn chat nhỏ:

![image](https://user-images.githubusercontent.com/87920408/194206480-378c7282-ecff-4046-ae62-9c21debc6d0f.png)

Có thể thấy đoạn text mà chúng ta cần decode là: `SdepaDwp{g3i_yd@jd_d0_p3u}`
Ngay đề bài đã có nhắc đến decode passwd và tên đề liên quan đến Ceasar. Chúng ta có thể dùng trang decode mật mã Ceasar này. Chúng ta sẽ cho chạy bruteforce để tìm ra passwd. Dựa vào format đề bài là WhiteHat{}

-–> `WhiteHat{k3m_ch@nh_h0_t3y}`

### [crypto05-RSA]
![image](https://user-images.githubusercontent.com/87920408/194207327-acc4bdfc-368c-4393-b2c9-4117f89e901a.png)

Tiến hành tải file: 

```python
n1 = 22863890244905355329502218444879121992098967068885212567588832322550382269571565476722229804216790522614182986234265447480480343340056180566597327262374522569117414826955679747486113074076465468667283056121308218220999527806457552463818309423361061235047300699782063457201514653614039159966459675409621953586146091231095743649548825118937476086468617169918285492379052546748768909781454820097333293111067375755986638189670886091656813282825101928290490818507170221784980336946980401043190939317871087400436267561251842806560316003269594317264541908976843604622916612938397771819876218019609569811408087863928944739859
n2 = 25396834019528394640490541529600980922556117537438324038107125716298569990777248043066348967684236346894506759770227146549619207671751562062007330768481162637093975688682909167807919749582072320507591463121041163079102865771367435992415668638153187837308760037166747856933832106378140305308765541852838889522565034007153190524225141330109695667493844526830658201754219481830865831841336965245012965037720539791430918298660242994119733090496411675643908510757625606914559432576805118863906625455665301582481731545159511674195787561151946139919419636082690775190511208632393990834913000845076890831887255186835784042961
c1 = 2798792052596520306906487161506201765424253144083404926197470746547978562491955280164116323131693186099978677526651582130224146487924351500545757146209936518426482010371233341915851760365345316274802099517947284381607367637094400400405556888988109812081793717754725797136387614194368932966293321060057732367203512692288477818772353036431885666452035969221909268918287387499047857827190445790533284679221173200372436186499972243598616552288964557913908366130105334086059520809750893401323863112255857590960198718923416134048795210311476282103438889124183978132887302326701513155679215589455661184313859734527448361504
c2 = 11900934425575667676450495319627600558858886958379867022500122866710884877898871454939798570379571002557158224443514436359517824471900092142427117331139646250231635461356384474600784706693799046330875256351965023512944154261251426235511574316879719010312298346194007737530280411868165472424304158601012005756054876357925827274607518823449615792476822622315467435634643981046538818199679947943147388703647928775473840965549565191934261229058389441930870957306398546961351382612103093447028587644220318369842912497497694698466843444750923988948597077647164728625973186393574052980795358021421364899621646547606467631974
e = 65537
```

Code giải: 
```python
from gmpy2 import mul, gcd
from Crypto.Util.number import inverse, long_to_bytes, bytes_to_long
N1 = 22863890244905355329502218444879121992098967068885212567588832322550382269571565476722229804216790522614182986234265447480480343340056180566597327262374522569117414826955679747486113074076465468667283056121308218220999527806457552463818309423361061235047300699782063457201514653614039159966459675409621953586146091231095743649548825118937476086468617169918285492379052546748768909781454820097333293111067375755986638189670886091656813282825101928290490818507170221784980336946980401043190939317871087400436267561251842806560316003269594317264541908976843604622916612938397771819876218019609569811408087863928944739859
N2 = 25396834019528394640490541529600980922556117537438324038107125716298569990777248043066348967684236346894506759770227146549619207671751562062007330768481162637093975688682909167807919749582072320507591463121041163079102865771367435992415668638153187837308760037166747856933832106378140305308765541852838889522565034007153190524225141330109695667493844526830658201754219481830865831841336965245012965037720539791430918298660242994119733090496411675643908510757625606914559432576805118863906625455665301582481731545159511674195787561151946139919419636082690775190511208632393990834913000845076890831887255186835784042961
ct1 = 2798792052596520306906487161506201765424253144083404926197470746547978562491955280164116323131693186099978677526651582130224146487924351500545757146209936518426482010371233341915851760365345316274802099517947284381607367637094400400405556888988109812081793717754725797136387614194368932966293321060057732367203512692288477818772353036431885666452035969221909268918287387499047857827190445790533284679221173200372436186499972243598616552288964557913908366130105334086059520809750893401323863112255857590960198718923416134048795210311476282103438889124183978132887302326701513155679215589455661184313859734527448361504
ct2 = 11900934425575667676450495319627600558858886958379867022500122866710884877898871454939798570379571002557158224443514436359517824471900092142427117331139646250231635461356384474600784706693799046330875256351965023512944154261251426235511574316879719010312298346194007737530280411868165472424304158601012005756054876357925827274607518823449615792476822622315467435634643981046538818199679947943147388703647928775473840965549565191934261229058389441930870957306398546961351382612103093447028587644220318369842912497497694698466843444750923988948597077647164728625973186393574052980795358021421364899621646547606467631974
e1 = 65537
e2 = 65537

def ProductTree(s):
    l = len(s)
    while l > 1:
        if l & 1 != 0:
            s += [1]
            l += 1
        s = list(map(mul, s[0: l >> 1], s[l >> 1:]))
        l = len(s)
    return s[0]

def Find_factor(pubs):
    priv_keys = []
    M = ProductTree(pubs)

    for i in range(0, len(pubs) - 1):
        pub = pubs[i]
        R = M // pub
        g = gcd(pub, R)
        if pub > g > 1:
            try:
                p = g
                q = pub // g
                return p, q
            except Exception as ex:
                print(ex)
                continue

p1, q1 = Find_factor([N1, N2])
p2, q2 = Find_factor([N2, N1])

n1 = p1*q1
n2 = p2*q2

phi1 = (p1-1) * (q1-1)
phi2 = (p2-1) * (q2-1)


d1 = inverse(e1, phi1)
d2 = inverse(e2, phi2)

m1 = pow(ct1, d1, n1)
m2 = pow(ct2, d2, n2)

print(long_to_bytes(m1)+long_to_bytes(m2))
```

--> `WhiteHat{I_h4t3_d0g_d4y_0f_5umm3rrr}`

### [crypto02-Programmer]
```python
from secret import flag

def cal_flag(flag):
	output=[]
	for i in range(len(flag)):
	    temp = ord(flag[i])**17%3233
	    output.append(temp)
	print(output)

if __name__ == '__main__':
	cal_flag(flag)

#[604, 2170, 3179, 884, 1313, 3000, 1632, 884, 855, 3179, 119, 1632, 2271, 119, 612, 2412, 2185, 2923, 2412, 1632, 2271, 2271, 1313, 2412, 119, 3179, 119, 2170, 1632, 2578, 1313, 119, 2235, 2185, 119, 745, 3179, 1369, 1313, 1516]
```
Đọc kỹ đề có thể thấy từ việc ta có 1 flag cho sẵn của đề –> ta sẽ biến đổi từng phần tử flag qua hàm `cal_flag`

Ta tiến hành viết lại code để chuyển đổi từng số trong output trở lại thành flag

Code đối chiếu các phần tử ascii từ `A` đến `}` thành các số trong output:
```python
for i in range(ord('A'), ord('}')+1):
    a[j] = i**17 % 3233
    print(chr(i), a[j])
    j += 1
 ```
 
 --> `WhiteHat{i_am_programmer_i_have_no_life}`
