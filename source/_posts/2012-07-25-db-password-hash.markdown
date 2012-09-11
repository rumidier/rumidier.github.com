---
layout: post
title: "DB_Password_Hash"
date: 2012-07-25 16:41
comments: true
categories: Catalyst Perl Password
---

## DB Password HASH

[DBIx::Class::EncodedColumn](https://metacpan.org/module/DBIx::Class::EncodedColumn)

기본 입력값 입력시 sha('password')사용 하여 암호화 할수 있도록 한다.

```
INSERT INTO `user` VALUES (2,'rum_user','rum_user@mail.com',sha('Password'),localtime ,localtime);
```

MyWeb::ResultBase.pm에 EncodedColumn 추가하여 준다.

```
__PACKAGE__->load_components(qw/
    EncodedColumn
    InflateColumn::DateTime
    TimeStamp
/);
```

[Catalyst::Plugin::Authentication](https://metacpan.org/module/Catalyst::Plugin::Authentication)

my_web.conf 파일에 플러그인 설정 추가
pawword_type 설정시 디폴트로 SHA-1이 적용되지만
명시적으로 password_hash_type을 정의 하여 준다.

```
<Plugin::Authentication>
    <default>
        password_type      hashed
        password_hash_type SHA-1
        user_model         DonDB::User
        class              SimpleDB
    </default>
</Plugin::Authentication>
```

### 설정 추가 참고 자료

[Catalyst::Authentication::Credential::Password](https://metacpan.org/module/Catalyst::Authentication::Credential::Password)

[Digest](https://metacpan.org/module/Digest#new)
