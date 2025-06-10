# Trocar a página de redirecionamento
Se precisar trabalhar com TYP diferentes com base nos dados informados na LP:

O exemplo abaixo troca de acordo com o campo personalizado companytype:
```
<script>
$( "select[name='cf_companytype']" ).change(function() {
    var companytype = $( this ).val();
    console.log( companytype );
    if( companytype == "Brand" )
    {
        document.getElementById('conversion-form').dataset.assetAction = btoa("https://xxx1");
    }
    else if( companytype == "Retailer" || companytype == "Distributor" )
    {
        document.getElementById('conversion-form').dataset.assetAction = btoa("https://xxx2");
    }
    else{
        document.getElementById('conversion-form').dataset.assetAction = btoa("https://xxx3");
    }
});
</script>
```