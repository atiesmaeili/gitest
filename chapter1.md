# how to: check features

by modifying`cmake`build options, different algorithms and features can be added to \(or trimmed\) from the library.

to list all available features \(included in build\):

```
using
namespace
mbedcrypto
;
auto
 hashes = installed_hashes(); 
//
 returns std::vector
<
mbedcrypto::hasht_t
>

std::cout 
<
<
"
supports 
"
<
<
 hashes.size() 
<
<
"
 hash algorithms: 
"
;

for
 ( 
auto
 h : hashes ) { 
//
 print all installed hashes
//
 convert type to string

    std::cout 
<
<
to_string
(h) 
<
<
"
 , 
"
;
}


//
 similarly
auto
 paddings = installed_paddings();

auto
 bmodes   = installed_block_modes();

auto
 ciphers  = installed_ciphers();

auto
 pks      = installed_pks();

auto
 curves   = installed_curves();
```

`mbedcrypto`types are`enum class`es and are also accessible from string names:

```
//
 convert from string to a type
auto
 htype = from_string
<
hash_t
>
(
"
sha256
"
);

if
 ( htype != 
hash_t
::none ) {
}
```

to check for availability of a feature:

```
//
 check by type (enum class)
if
 ( supports(
cipher_t
::aes_256_cbc)   
&
&
   supports(
pk_t
::rsa) ) {
    
//
 do stuff

}

//
 check by algorithm name
if
 ( supports_hash(
"
sha1
"
)    
&
&
    supports_pk(
"
rsa
"
) ) {
    
//
 sign a message ...

}

//
 both upper and lower case are supported
if
 ( supports_cipher(
"
CAMELLIA_128_CBC
"
) ) {
}


//
 to check a single feature
if
 ( suppurts(features::aes_ni) ) {
    std::cout 
<
<
"
this system supports AESNI (hardware accelerated AES)
"
<
<
 std::endl;
}


if
 ( supports(features::aead)    
&
&
    supports(cipher_bm::gcm) ) {
    
//
 do GCM authenticated encryption with additional data

}
```

see[types.hpp](https://github.com/azadkuh/mbedcrypto/blob/master/include/mbedcrypto/types.hpp)



