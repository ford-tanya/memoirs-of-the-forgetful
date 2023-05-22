
# 🍀23 Step Deploy API Node.js in AWS EC2
การ Deploy API Node.js ลง AWS EC2

ผู้เขียน: [Ford Tanya](https://github.com/ford-tanya)

รุ่นพี่ผู้สอน: [Panwa Muangsong](https://github.com/panwazii)

1.  เปิด Windows PowerShell แบบ Run as administrator  
2. ```bash
	Get-WindowsCapability -Online | Where-Object Name -like 'OpenSSH*  
	  ```
	  ใช้ในการค้นหาว่า OpenSSH มีการติดตั้งในเครื่องคอมพิวเตอร์ที่ทำงานอยู่หรือไม่  
ถ้าคำสั่งคืนค่าผลลัพธ์ แสดงว่า OpenSSH มีการติดตั้งในระบบปฏิบัติการ Windows ที่ทำงานอยู่  
ถ้าไม่มีผลลัพธ์ที่แสดงขึ้นมา แสดงว่า OpenSSH ไม่ได้ถูกติดตั้งในระบบปฏิบัติการ Windows ที่ทำงานอยู่ 

3. ```bash
	ssh -i <path_of_key_pair> ubuntu@<IPv4_Server>  
	 ```
	เป็นคำสั่งที่ใช้ในการเชื่อมต่อเข้าสู่เซิร์ฟเวอร์โดยใช้ SSH และ key pair ที่ระบุ path โดย 

	| variable| ความหมาย |
	|-------------|---------------------|
	| `<path_of_key_pair>` | เป็นที่อยู่ directory ไฟล์ key pair สกุลไฟล์ .pem |
	|  `<IPv4_Server>`  | เป็น IP ของเซิร์ฟเวอร์ที่เราจะเข้า  |
   
>ubuntu เป็นชื่อ username ที่จะเข้าเซิร์ฟเวอร์ โดย “ubuntu” เป็นชื่อที่นิยมสำหรับการเชื่อมต่อเซิร์ฟเวอร์  สามารถเปลี่ยนชื่อได้  
	  
> สามารถเช็ค username ใน ubuntu ได้โดยใช้คำสั่ง whoami  

4. `ll` คำสั่งสำหรับแสดงรายการไฟล์และโฟลเดอร์ในพื้นที่ปัจจุบัน  

5. `pwd` คำสั่งสำหรับแสดง directory ที่ทำงานยู่ปัจจุบัน  

6. ```bash
	sudo apt update  
	 ```  
	 อัปเดทแพคเกจทั้งหมดเป็นข้อมูลล่าสุด  
	  
> การใช้คำสั่ง "sudo" ในการรันคำสั่งหมายความว่าให้สิทธิ์ผู้ดูแลระบบ (root) เพื่อติดตั้งแพคเกจในระบบ  ย่อมาจาก "superuser do"

> apt เป็นระบบการจัดการแพคเกจในระบบปฏิบัติการ ubuntu ย่อมาจาก "Advanced Packaging Tool" ซึ่งใช้สำหรับการติดตั้งและจัดการแพคเกจที่เกี่ยวข้องกับระบบปฏิบัติการ.  
  
> การใช้ apt ร่วมกับคำสั่ง sudo (superuser do) จะให้สิทธิ์ผู้ดูแลระบบ (root) เพื่อดำเนินการในระบบ ดังนั้นเราจะใช้คำสั่ง "sudo apt <คำสั่ง>" เพื่อดำเนินการในระบบปฏิบัติการ.  


7. ```bash
	sudo apt upgrade  
	 ```  
	ระบบจะดาวน์โหลดแพคเกจที่มีการอัปเกรดและนำมาติดตั้งเพื่อแทนที่เวอร์ชันเก่าที่ติดตั้งอยู่ 

8. ```bash
	sudo apt install nginx  
	 ```   
	 ใช้ในการติดตั้งเซิร์ฟเวอร์เว็บ Nginx  

	Nginx เป็นเว็บเซิร์ฟเวอร์ที่มีประสิทธิภาพสูงและยืดหยุ่น ทำหน้าที่ในการรับและส่งข้อมูลในระบบเครือข่าย  
หลังจากติดตั้งเสร็จแล้ว ให้ลองใช้ Public IPv4 address ของ server เปิดในบราวเซอร์แบบ http ก็จะแสดงข้อความนี้ให้เห็น

	Welcome to nginx!

	If you see this page, the nginx web server is successfully installed and working. Further configuration is required.
	...  
	
	ถ้าเห็นข้อความนี้ในบราวเซอร์หลังจากติดตั้ง Nginx หมายความว่า Nginx ติดตั้งและทำงานได้สำเร็จ  
	
9. ```bash
	sudo apt install nodejs
	 ``` 
	  ใช้ในการติดตั้ง Node.js  
Node.js เป็นแพลตฟอร์มการรันโปรแกรม JavaScript บนเซิร์ฟเวอร์หรือเครื่องคอมพิวเตอร์  


10. ```bash
	sudo apt install npm
	 ```
	การติดตั้งเครื่องมือจัดการแพคเกจของ Node.js (npm) เนื่องจากในระบบปฏิบัติการ Ubuntu การติดตั้ง Node.js ด้วยการใช้ apt (sudo apt install nodejs) อาจไม่รวม npm มาในการติดตั้งด้วย  

11. ทำการ clone โปรเจกต์ github โดยใช้คำสั่ง  
	```bash
	git clone https://<tokenhere>@github.com/<user>/<repo>.git
	 ```
	 | variable| ความหมาย |
	 |-------------|---------------------|
	 | `<tokenhere>` | Personal Access Token (PAT) ที่มีสิทธิ์เข้าถึงโปรเจกต์ โดยสร้างขึ้นใน GitHub|
	 | `<user>`  | ชื่อผู้ใช้ GitHub ที่เป็นเจ้าของโปรเจกต์ที่ต้องการคัดลอก  |
	 | `<repo>` | ชื่อของโปรเจกต์ที่ต้องการคัดลอก |
	
  
12. ```bash
	cd <clone project>
	 ``` 
	ใช้ในการเปลี่ยนไดเรกทอรี (directory) ไปยังโปรเจกต์ที่ได้คัดลอกมาจาก GitHub  


13. ```bash
	sudo nano package.json
	 ``` 
	 > ขั้นตอนนี้สำหรับโปรเจกต์ที่ยังตั้งค่าเป็น nodemon index.js อยู่

	ใช้ในการเปิดไฟล์ package.json ด้วยโปรแกรมที่ชื่อว่า nano  
ยกตัวอย่างการแก้ไขส่วนของ "scripts":  

	ก่อนแก้ไข:  
	
  	```bash
	"scripts": {
	"start": "nodemon index.js"
	} 
    ```
	หลังแก้ไข:
	  
  	```bash
	"scripts": {
	"start": "node index.js"
	} 
    ```
  
	ใช้คำสั่ง "ctrl+x" ในโปรแกรม nano ใช้ในการออกจากโหมดแก้ไขและเรียกใช้คำสั่งออกจากโปรแกรม nano  
เมื่อกดแล้ว โปรแกรม nano จะแสดงข้อความ "Save modified buffer?"  
และเราจะต้องตอบว่าต้องการบันทึกการเปลี่ยนแปลงที่ทำไว้หรือไม่
  
	ให้กดปุ่ม "Y" (ยืนยัน) เพื่อบันทึกการเปลี่ยนแปลงที่ได้ทำในไฟล์ package.json แล้วกด Enter  
cat package.json เพื่อแสดงเนื้อหาของไฟล์  

	การแก้ไขนี้จะทำให้เว็บแอปพลิเคชันไม่ใช้งาน "nodemon" และจะรันด้วย "node" แทน  
สำหรับการพัฒนาของแอปพลิเคชัน เราสามารถติดตั้ง "nodemon" ในระหว่างการพัฒนาเพื่อให้  
ได้ประโยชน์จากการรีโหลดอัตโนมัติของแอปพลิเคชันของคุณเมื่อไฟล์มีการเปลี่ยนแปลง  

	แต่ในการใช้งานโปรดักชัน (production) ควรใช้ "node" เพื่อป้องกันการรีโหลดไม่จำเป็นของแอปพลิเคชัน  ในเซิร์ฟเวอร์ที่ให้บริการจริง

  

15. ```bash
	npm i
	 ```
	เป็นคำสั่งสำหรับติดตั้งแพคเกจ (packages) ที่ระบุในไฟล์ package.json ของโปรเจกต์
> เป็นคำสั่งย่อจาก npm install สามารถใช้ได้เหมือนกันทั้งคู่
	
16. ถ้าเกิดติดตั้งแล้วเจอปัญหาเกี่ยวข้องกับเวอร์ชั่นของ Node.js ที่ไม่สอดคล้องกับความต้องการของแพคเกจที่ระบุในไฟล์ package.json อย่างเช่น
    ```bash
	 ubuntu@ip-172-31-26-123:~/helpdesk-api-modularization-deploy$ sudo npm i
     npm WARN EBADENGINE Unsupported engine {
     npm WARN EBADENGINE  package: 'lru-cache@8.0.5',
     npm WARN EBADENGINE  required: { node: '>=16.14' },
     npm WARN EBADENGINE  current: { node: 'v12.22.9', npm: '8.5.1' }
     npm WARN EBADENGINE }
	 ```

แพคเกจ lru-cache@8.0.5 ต้องการ Node.js รุ่น 16.14 หรือสูงกว่า ในขณะที่ Node.js ที่ใช้เป็นรุ่น 12.22.9 เราจึงต้องอัปเดต Node.js เป็นรุ่นที่เข้ากันได้ก่อน

16.1. ติดตั้ง nvm (ถ้ายังไม่ได้ติดตั้ง):  
```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash
```

16.2. ปิดและเปิดเทอร์มินอลใหม่หรือใช้คำสั่ง `source ~/.bashrc` เพื่อโหลดการตั้งค่าใหม่
16.3. ตรวจสอบรุ่น Node.js ที่พร้อมใช้งาน:  `nvm ls-remote`
16.4. เลือกและติดตั้งรุ่น Node.js ที่เข้ากันได้:  `nvm install 16.14`
16.5. ตั้งค่าให้ใช้รุ่น Node.js ที่เพิ่งติดตั้ง:  `nvm use 16.14`
16.6. เช็คเวอร์ชั่น node ที่ใช้ในปัจจุบัน: `node -v`
16.7. npm start ถ้าไม่มีปัญหาเกิดขึ้นโปรแกรมรันผ่านแปลว่าโอเครแล้ว

17. ```bash
	sudo nano /etc/nginx/sites-available/default
	 ```  
	ใช้ในการเปิดแก้ไขไฟล์ default configuration ของ Nginx ซึ่งอยู่ในที่ตั้ง /etc/nginx/sites-available/default.

	ลบโค้ดทั้งหมดโดยกด ctrl+k แล้วเปลี่ยนวางโค้ดต่อไปนี้

	   ```bash
		server {
			listen 80;
			
			server_name <IPv4_Server>;
			location / {
				proxy_set_header  Host $host;
				proxy_set_header  X-Real-IP $remote_addr;
				proxy_set_header  X-Forwarded-For $proxy_add_x_forwarded_for;
				proxy_set_header  X-Forwarded-Proto $scheme;
				proxy_set_header  X-NginX-Proxy true;
				
				proxy_pass http://localhost:8000/;
				proxy_http_version 1.1;
				proxy_redirect http://localhost:8000/ https://%24server_name/;
			}
		}
	```

	หลังจากนั้นกดออกและบันทึก  

	โดยปกติแล้ว, Nginx จะเป็นตัวกลาง (reverse proxy) ที่ส่งการร้องขอ (request) ที่มาที่พอร์ต 80 ไปยังเซิร์ฟเวอร์ที่ทำงานอยู่ใน localhost ที่พอร์ต 8000 ซึ่งเป็นพอร์ตที่โปรเจกต์รัน
	  
	และโค้ด proxy_redirect จะกำหนดให้เรียกใช้ URL ที่มีโพรโทคอล HTTPS และเซิร์ฟเวอร์เป็นค่าของตัวแปร $server_name.  
	  
	%24 ในที่นี้เป็นการเขียนรหัสของตัวแปร $ ในรูปแบบของ URL Encoding. เมื่อ Nginx ดำเนินการประมวลผลโค้ดนี้ จะแทนที่ %24 ด้วยตัวแปร $server_name ใน URL เป็นค่าที่ถูกต้อง.

  

18. ```bash
	cat /etc/nginx/sites-available/default 
    ```  
	ใช้ในการแสดงเนื้อหาของไฟล์ default configuration ของ Nginx  

19. ```bash
	 sudo systemctl restart nginx 
    ```
	ใช้ในการรีสตาร์ท (restart) เซิร์ฟเวอร์ Nginxหลังจากรีสตาร์ทเสร็จแล้ว ลองใช้ Public IPv4 address ของ server เปิดในบราวเซอร์แบบ http  ก็จะเห็นข้อความขึ้นว่า  
	
	502 Bad Gateway
	nginx/1.18.0 (Ubuntu)  

	กลับไปรันโปรแกรม npm start แล้วไป refresh บราวเซอร์ก็จะเห็นข้อความของโปรแกรมเราแล้ว

20. ```bash
	 sudo npm i pm2 -g 
    ``` 
	ใช้ในการติดตั้งเครื่องมือ PM2 ที่เป็นเครื่องมือจัดการกระบวนการ (process manager) ของ Node.js ซึ่งติดตั้งในรูปแบบ Global (-g) 

21. ```bash
	 pm2 status
    ```
    ใช้ในการแสดงสถานะของกระบวนการที่ PM2 กำลังจัดการอยู่ในปัจจุบัน  

22. ```bash
	 pm2 start npm --name "<name>" -- start
    ``` 
	ใช้ในการเริ่มกระบวนการการทำงานของโปรเจกต์ที่ต้องการด้วยใช้งาน PM2. โดย `<name>` จะเป็นชื่อที่ต้องการให้ PM2 ใช้เป็นชื่อของกระบวนการในการจัดการโปรเจกต์.  


	ในการใช้คำสั่ง `pm2 start npm --name "<clone project>" -- start` เราต้องใช้คำสั่งในไดเรกทอรีที่เป็นโปรเจกต์นั้นๆ เพื่อให้ PM2 สามารถเริ่มต้นกระบวนการการทำงานของโปรเจกต์ดังกล่าวได้ถูกต้อง.

	หลังจากแสดงตารางแล้วมี status ‘online’ หมายความว่าโปรแกรมรันทำงานแล้ว  

23. ถ้าอยากให้ PM2 ถูกเรียกใช้งานโดยอัตโนมัติเมื่อเซิร์ฟเวอร์เริ่มทำงานใหม่ใน Ubuntu (รุ่น 16.04 หรือสูงกว่า) สามารถใช้คำสั่งต่อไปนี้เพื่อสร้างสคริปต์ init สำหรับ PM2:  
	```bash
	pm2 startup  
	```

	PM2 จะสร้างสคริปต์ init ที่จะทำการเรียกใช้งาน PM2 พร้อมกับกระบวนการที่อยู่ใน PM2 เมื่อระบบเริ่มต้นขึ้นใหม่  ตัวอย่างผลลัพธ์ที่แสดงหลังจากคำสั่ง pm2 startup คือ:  
	```bash
	 [PM2] Init System found: systemd
	 [PM2] To setup the Startup Script, copy/paste the following command:
	 sudo env PATH=$PATH:/usr/bin /usr/local/lib/node_modules/pm2/bin/pm2 startup systemd -u ubuntu --hp /home/ubuntu  
	```


	ในที่นี้เราจะต้องทำการคัดลอกและวางคำสั่งที่แสดงขึ้นบนหน้าจอ และทำการรัน  
  
	หลังจากนั้น เราสามารถใช้ pm2 save เพื่อบันทึกกระบวนการที่กำหนดไว้ใน PM2 ในระบบ init เพื่อให้เริ่มต้นต่อมาได้โดยอัตโนมัติเมื่อเซิร์ฟเวอร์เริ่มทำงานใหม่

