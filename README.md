# Introduction
This code checks validity of Iranian NationalCode.

```
function isValid(nationalCode) {
    if (!/^\d{10}$/.test(nationalCode))
        return false;
    var check = parseInt(nationalCode[9]);
    var sum = 0;
    var i;
    for (i = 0; i < 9; ++i) {
        sum += parseInt(nationalCode[i]) * (10 - i);
    }
    sum %= 11;

    return (sum < 2 && check == sum) || (sum >= 2 && check + sum == 11);
}
```

This code checks validity of Iranian IBAN.
```
function modulo(aNumStr, aDiv) {
    var tmp = "";
    var i, r;
    for (i = 0; i < aNumStr.length; i++) {
        tmp += aNumStr.charAt(i);
        r = tmp % aDiv;
        tmp = r.toString();
    }
    return tmp / 1;
}


function isValid(iban) {
    if (iban.length === 26 && iban.startsWith("IR", 0)) {
        //Move front 4 digits to the end
        var rearrange =
            iban.substring(4, iban.length) + iban.substring(0, 4);

        var alphabet = "ABCDEFGHIJKLMNOPQRSTUVWXYZ".split("");
        var alphaMap = {};
        var number = [];
        $.each(alphabet,
            function(index, value) {
                alphaMap[value] = index + 10;
            });

        $.each(rearrange.split(""),
            function(index, value) {
                number[index] = alphaMap[value] || value;
            });

        return modulo(number.join("").toString(), 97) === 1;
    } else return false;
}
```
