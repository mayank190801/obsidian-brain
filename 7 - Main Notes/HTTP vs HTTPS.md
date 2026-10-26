
2024-06-27 18:51
Status: 
Tags: [[4 - Tags/system design|system design]] [[networks]]

# HTTP vs HTTPS

HTTP
1. **No Encryption**: HTTP does not encrypt the data being transmitted. This means that the data can be intercepted and read by others.
2. **Default Port**: It typically operates over port 80.
3. **Vulnerabilities**: More vulnerable to man-in-the-middle attacks and eavesdropping.

HTTPS
1. **Encryption**: HTTPS encrypts the data being transmitted using protocols like SSL (Secure Sockets Layer) or TLS (Transport Layer Security). This encryption ensures that even if the data is intercepted, it cannot be easily read by attackers.
2. **Default Port**: It operates over port 443.
3. **Trustworthiness**: Websites with HTTPS are generally trusted more by users. Browsers often mark HTTP sites as 'Not Secure'.
###### Key Differences:
1. **Security**: The most significant difference is security. HTTPS provides a secure layer through encryption, while HTTP does not.
2. **Performance**: HTTPS may cause slightly more server load due to the encryption and decryption process.
3. **SEO Ranking**: Search engines like Google give preference to HTTPS websites, considering them more secure.
4. **Certificate Requirement**: To implement HTTPS, a website must obtain an SSL/TLS certificate from a Certificate Authority (CA).


# **References**