# 日本食品標準成分表2020年版(八訂)をjson形式にしたものです

2020年12月25日に文部科学省が公開した[日本食品標準成分表2020年版(八訂)](https://www.mext.go.jp/a_menu/syokuhinseibun/mext_01110.html)を元に作成しています。  
日本食品標準成分表とは、食品可食部100gあたりの成分の含有量を示すものです。普段手に取る食料品の裏側に表記されている栄養価は、基本的にこのデータを元に計算されています。  
しかしながら、このデータは機械判読不可能な.xlsxでしか提供されておらず、プログラムで利用するとなると、セルの結合の解除や、改行コード、全角スペースの削除など本質的ではない作業から始めることになります。このオープンデータを利用して何かをつくろうとする方の一助になれば幸いです。  
  
リポジトリの名前は、日本食品標準成分表2020年版(八訂)の旧版である、日本食品標準成分表2015年版(七訂)の英語版[Standards Tables of Food Composition in Japan -2015- (Seventh Revised Edition)](https://www.mext.go.jp/en/policy/science_technology/policy/title01/detail01/sdetail01/sdetail01/1385122.htm)からです。  

## todo
* tagnamesをkeyにすると直感的でない
* 'Tr'と'-'をnullと表記している
* 単位のデータをどこに入れるか
* ヨウ素(iodine)のkeyが'id'になってしまい、何かと衝突する場合がありそう
  
## 構成
tagnames(成分識別子)のキャメルケースをkeyとして作成しました。(直感的でないのですが英語をそのままKeyにしようとなると、例えば`protcaa`は`Protein, calculated as  the sum of amino acid residues`になってしまいます。)  
tagnameには末尾に'-'が付くものがありますが、その'-'は削除しています(厳密には意味が異なってしまうため検討の余地があります。)  

例  
```json
{
    "groupId": 1,
    "foodId": 1001,
    "indexId": 1,
    "foodName": "アマランサス 玄穀",
    "refuse": 0,
    "enerc": 1452,
    "enercKcal": 343,
    "water": 13.5,
    "protcaa": 11.3,
    "prot": 12.7,
    "fatnlea": 5,
    "chole": 0,
    "fat": 6,
    "choavlm": 63.5,
    "choavl": 57.8,
    "choavldf": 59.9,
    "fib": 7.4,
    "polyl": null,
    "chocdf": 64.9,
    "oa": null,
    "ash": 2.9,
    "na": 1,
    "k": 600,
    "ca": 160,
    "mg": 270,
    "p": 540,
    "fe": 9.4,
    "zn": 5.8,
    "cu": 0.92,
    "mn": 6.14,
    "id": 1,
    "se": 13,
    "cr": 7,
    "mo": 59,
    "retol": 0,
    "carta": 0,
    "cartb": 2,
    "crypxb": 0,
    "cartbeq": 2,
    "vitaRae": null,
    "vitD": 0,
    "tocphA": 1.3,
    "tocphB": 2.3,
    "tocphG": 0.2,
    "tocphD": 0.7,
    "vitK": 0,
    "thia": 0.04,
    "ribf": 0.14,
    "nia": 1,
    "ne": 3.8,
    "vitB6A": 0.58,
    "vitB12": 0,
    "fol": 130,
    "pantac": 1.69,
    "biot": 16,
    "vitC": 0,
    "alc": null,
    "naclEq": 0
}
```
  
### tagname/成分識別子とは
FAO/INFOODSが定めている栄養素の識別子です。  
日本食品標準成分表2020年版(八訂)の成分識別子は、完全には準拠しておらず表記に振れがあります。  
そのため日本独自のtagnamesと解釈したほうが良いでしょう。  
参考:[日本食品標準成分表に関するQ&A](https://www.mext.go.jp/a_menu/syokuhinseibun/__icsFiles/afieldfile/2017/02/22/QA_2015.pdf)  
[FAO/INFOODS Databases Analytical food composition database Version 2.0 – AnFooD2.0 User guide](http://www.fao.org/3/a-i7360e.pdf)  
  
## 対応表

| 栄養素名              | tagnames   | key       | 単位   |
| ----------------- | ---------- | --------- | ---- |
| 廃棄率               | REFUSE     | refuse    | %    |
| エネルギー(kJ)         | ENERC      | enerc     | kJ   |
| エネルギー(kcal)       | ENERC_KCAL | enercKcal | kcal |
| 水分                | WATER      | water     | g    |
| アミノ酸組成によるたんぱく質    | PROTCAA    | protcaa   | g    |
| たんぱく質             | PROT-       | prot      | g    |
| 脂肪酸のトリアシルグリセロール当量 | FATNLEA    | fatnlea   | g    |
| コレステロール           | CHOLE      | chole     | mg   |
| 脂質                | FAT-        | fat       | g    |
| 利用可能炭水化物(単糖当量)    | CHOAVLM    | choavlm   | g    |
| 利用可能炭水化物(質量計)     | CHOAVL     | choavl    | g    |
| 差引き法による利用可能炭水化物   | CHOAVLDF-   | choavldf  | g    |
| 食物繊維総量            | FIB-        | fib       | g    |
| 糖アルコール            | POLYL      | polyl     | g    |
| 炭水化物              | CHOCDF-     | chocdf    | g    |
| 有機酸               | OA         | oa        | g    |
| 灰分                | ASH        | ash       | g    |
| ナトリウム             | NA         | na        | mg   |
| カリウム              | K          | k         | mg   |
| カルシウム             | CA         | ca        | mg   |
| マグネシウム            | MG         | mg        | mg   |
| リン                | P          | p         | mg   |
| 鉄                 | FE         | fe        | mg   |
| 亜鉛                | ZN         | zn        | mg   |
| 銅                 | CU         | cu        | mg   |
| マンガン              | MN         | mn        | μg   |
| ヨウ素               | ID         | id        | μg   |
| セレン               | SE         | se        | μg   |
| クロム               | CR         | cr        | μg   |
| モリブデン             | MO         | mo        | μg   |
| レチノール             | RETOL      | retol     | μg   |
| α カロテン            | CARTA      | carta     | μg   |
| β カロテン            | CARTB      | cartb     | μg   |
| β クリプトキサンチン       | CRYPXB     | crypxb    | μg   |
| β カロテン当量          | CARTBEQ    | cartbeq   | μg   |
| レチノール活性当量         | VITA_RAE   | vitaRae   | μg   |
| ビタミン D            | VITD       | VitD      | μg   |
| α トコフェロール         | TOCPHA     | tocphA    | mg   |
| β トコフェロール         | TOCPHB     | tocphB    | mg   |
| γ トコフェロール         | TOCPHG     | tocphG    | mg   |
| δ トコフェロール         | TOCPHD     | tocphD    | mg   |
| ビタミン K            | VITK       | vitK      | μg   |
| ビタミン B1           | THIAHCL    | thiahcl   | mg   |
| ビタミン B2           | RIBF       | ribf      | mg   |
| ナイアシン             | NIA        | nia       | mg   |
| ナイアシン当量           | NE         | ne        | mg   |
| ビタミン B6           | VITB6A     | vitB6A    | mg   |
| ビタミン B12          | VITB12     | vitB12    | μg   |
| 葉酸                | FOL        | fol       | μg   |
| パントテン酸            | PANTAC     | pantac    | mg   |
| ビオチン              | BIOT       | biot      | μg   |
| ビタミン C            | VITC       | vitC      | mg   |
| アルコール             | ALC        | alc       | g    |
| 食塩相当量             | NACL_EQ    | naclEq    | g    |


## keyを変えたいとき
/csvの中に日本語、英語、成分識別子(tagnames)を入れておいたのでbodyとくっつけて
```
npx csvtojson --checkType=true hoge.csv > fuga.json
```
などとして生成してください。  

## LICENCE
[CC BY 4.0](LICENCE.md)  
[文部科学省ウェブサイト利用規約](https://www.mext.go.jp/b_menu/1351168.htm)
