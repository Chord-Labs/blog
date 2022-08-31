function getFullNum(num){
    if(isNaN(num)){return num};
    var str = ''+num;
    if(!/e/i.test(str)){return num;};
    return (num).toFixed(18).replace(/\.?0+$/, "");
}
