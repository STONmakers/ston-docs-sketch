.. _imagelog:

HTTPS
******************

Fallback 인증서
====================================

ECDSA로 서명된 인증서는 RSA로 서명된 인증서에 비해 성능상의 이점을 가진다. 
`SSL.com <https://www.ssl.com/>`_ 의 `Comparing ECDSA vs RSA <https://www.ssl.com/article/comparing-ecdsa-vs-rsa/>`_ 에 따르면 112 bit레벨의 암호화에서 RSA는 2048 bit의 키가 필요한 반면 ECDSA는 224 bit 키만으로도 충분한다. 
128bit 레벨의 암호화에선 RSA의 상황이 더 나빠지는데, RSA는 3072 bit, ECDSA는 256 bit가 필요하다. 
결론적으로 보안레벨이 높아질수록 RSA는 효율적이지 못한 옵션이 된다. ::

                                sign/s
    256 bit ecdsa (nistp256)    9516.8
    rsa 2048 bits               1001.8

    (openssl 1.0.2 beta on x86_64 with enable-ec_nistp_64_gcc_128)

<출처. `Cloudflare - ECDSA: The digital signature algorithm of a better internet <https://blog.cloudflare.com/ecdsa-the-digital-signature-algorithm-of-a-better-internet/>`_ >

AWS CloudFront도 2018년부터 `ECDSA를 통한 원본서버 연결을 지원 <https://aws.amazon.com/ko/about-aws/whats-new/2018/03/cloudfront-now-supports-ecdsa-certificates-for-https-connections-to-origins/>`_ 하는등 시장에 널리 도입되고 있다.

ECDSA 인증서를 도입하는 가장 큰 걸림돌은 TLS 클라이언트의 Cipher Suite 호환성이다. 
ECDSA는 TLS 1.2부터 표준이 되었기 때문에 이를 미지원하는 클라이언트가 아직 존재하며 이들은 HTTPS 세션 연결이 불가능하다.

이런 문제로 인해 해결하기 위해 한 주체(Subject)에 대해 다중 인증서를 지원하는 상황이 발생한다. ::

   <Https>
      <Cert>/usr/ssl/cert_ecdsa.pem | /usr/ssl/cert_rsa.pem</Cert>
      <Key>/usr/ssl/certkey_ecdsa.pem | /usr/ssl/certkey_rsa.pem</Key>
      <CA>/usr/ssl/ca_ecdsa.pem | /usr/ssl/ca_rsa.pem</CA>
   </Https>

다중 인증서는 파이프("|")로 구분하며 동작 시나리오는 다음과 같다.

   - ECDSA를 지원하는 클라이언트라면 cert_ecdsa.pem 인증서를 제공한다.
   - 지원하지 않는다면 다음 인증서인 cert_rsa.pem 인증서를 제공한다.

