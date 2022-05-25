# 프로젝트 설명
기존에 python으로 작업한 프로젝트를 java 프로젝트로 리펙토링  
기존 github link (https://github.com/unfunhy/MakeYourPortfolio)


# 기술 스택
### Backend
- 변경 전: Python, Flask, Sqlalchemy, MySQL
- 변경 후: Java, Spring, Spring Data JPA, MySQL, H2
### Frontend
- Javascript, React, Styled component, Axios
- 변경 사항 없음
### 사용자 인증 방식
- 변경 전: JWT
- 변경 후: Session

api의 경우에도 일부 변경 사항 있음, 변경 전 api 정보는 이전 레포의 README 확인

# Rest API
##### get_user_info
URI = "/login"    
METHODS = ["GET"]  
headers = { Authorization }  
response = { id, name }
desc = sessionId로 유저 id, name 확인용 api
##### login
URI = "/login"  
METHODS = ["POST"]  
data = { email, user_pw }  
response = { Authorization, id, name}  
desc = 유저 로그인 api, response에 sessionId 포함 
##### check_email
URI = "/register"  
METHODS = ["GET"]  
parmas = { email }
desc = email 중복 여부 확인    
##### register
URI = "/register"  
METHODS = ["POST"]  
data = {user_id, user_pw}
##### get_portfolio_list
URI = "/portfolios"  
METHODS = ["GET"]  
params = { search }  
response = { userInfo: { [id, introduce, name, profile], ... } }  
desc = 네트워크 페이지 유저 정보 api
##### get_portfolio
URI = "/portfolio"   
METHODS = ["GET"]  
headers, params = { Authorization, id }
response = { user, education, award, project, certificate }  
desc = 특정 유저의 상세 포트폴리오 페이지 열람 api
##### update_portfolio
URI= "/portfolio/user"   METHODS=["PATCH"]   headers={ Authorization }  response = {target, target_id, ...}  
URI= "/portfolio/profile"   METHODS=["PATCH"]   headers={ Authorization }  response = {target, target_id, ...}  
URI= "/portfolio/education"   METHODS=["PATCH"]   headers={ Authorization }  response = {target, target_id, ...}  
URI= "/portfolio/award"   METHODS=["PATCH"]   headers={ Authorization }  response = {target, target_id, ...}  
URI= "/portfolio/project"   METHODS=["PATCH"]   headers={ Authorization }  response = {target, target_id, ...}  
URI= "/portfolio/certificate"   METHODS=["PATCH"]   headers={ Authorization }  response = {target, target_id, ...}
##### delete_information
URI= "/portfolio/education"   METHODS=["DELETE"]   headers={ Authorization }  
URI= "/portfolio/award"   METHODS=["DELETE"]   headers={ Authorization }  
URI= "/portfolio/project"   METHODS=["DELETE"]   headers={ Authorization }  
URI= "/portfolio/certificate"   METHODS=["DELETE"]   headers={ Authorization }
##### get_static_img
URI= "/img"   METHODS=["GET"]   PARAMS=imgSrc


# DB Schema
```
Table User {  
    id,          (int, pk, fk)  
    email,       (varchar(32))  
    user_pw,     (binary(60))  
    name,        (varchar(16))  
    introduce    (varchar(128))  
    profile      (varchar(128))
    register_date, (datetime)  
}
```

```
Table Education {  
    id,          (int, pk)  
    user_id,     (int, fk)  
    school,      (varchar(128))  
    major,       (varchar(128))  
    state,       (char(1))  
}  
Table education_state{
    id,          (int, pk)
    state        (varchar(16))
}
```

```
Table Award {  
    id,          (int, pk)  
    user_id,     (int, fk)  
    title,       (varchar(128))  
    desc,        (text)  
}  
```

```
Table Project {  
    id,          (int, pk)  
    user_id,     (int, fk)  
    title,       (varchar(128))  
    desc,        (text)  
    start,       (date)  
    end,         (date)  
}  
```

```
Table Certificate {  
    id,          (int, pk)  
    user_id,     (int, fk)  
    title,       (varchar(128))  
    auth,        (varchar(128))  
    acq_date     (date)  
}  
```
