## WSDL to PHP with Auth

```php
<?php

    //ini_set("soap.wsdl_cache_enabled", "0");

    $client = new SoapClient("soap-api-url.asmx?wsdl",[
        'soap_version'=>SOAP_1_2,
        'exceptions'=>true,
        'trace'=>1,
        'cache_wsdl'=>WSDL_CACHE_NONE,
    ]);

    $headerbody = array(
        'KullaniciAdi'=> '',
        'Sifre'=> ''
    ); 
    $header = new SoapHeader('http://tempuri.org/', 'SecuredWebServiceHeader', $headerbody);       

    $client->__setSoapHeaders($header);

    try {
        $result = $client->HavaleYap([
             'GonderenMusteriNo' => '',
             'GonderenEkno' => '',
             'AliciMusteriNo' => '',
             'AliciEkno' => '',
             'iban' => '',
             'DovizCinsi' => '',
             'Tutar' => '',
             'Aciklama' => '',
             'MusteriReferans' => '',
             'TCKNVKN' => '',
             'odemeNedeni' => '',
             'aliciHesapKapaliysaAcikHesabiBul' => '',
        ]);
        if ($result->HavaleYapResult) {
            print_r($result->HavaleYapResult->CevapMesaji);
            //echo 'TRUE';
        } else {
            echo 'FALSE';
        }
    } catch (Exception $e) {
        dd($e);
    }

?>
```