<template>
  <div id="app">
    <tabler :values="values" :config="config" :nb_visible_cols="7">
<!--      <template v-slot:col-head-test>Test head</template>-->
      <template v-slot:col-value-gender="slotProps" >Ma valeur {{ slotProps.line.gender}}</template>
    </tabler>
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css" integrity="sha384-Gn5384xqQ1aoWXA+058RXPxPg6fy4IWvTNh0E263XmFcJlSAwiGgFAW/dAiS6JXm" crossorigin="anonymous">
  </div>
</template>

<script>
import Tabler from './components/Tabler'
import Tabler2 from "./components/Tabler2";

export default {
  name: 'app',
  components: {
    Tabler2,
    Tabler,
  },
  data() {
    return {
      values: [
        {
          "_id": "5d8ca4d3fce2881aa0c3e811",
          "isActive": true,
          "balance": "$1,742.50",
          "age": 33,
          "eyeColor": "blue",
          "lastname": " Gilbert",
          "firstname": "Wanda",
          "gender": "female",
          "company": "COMBOGENE",
          "email": "wandagilbert@combogene.com",
          "phone": "+1 (870) 578-3839",
          "address": "570 Gunther Place, Falconaire, Kansas, 3207",
          "about": "Do anim ex proident Lorem tempor dolor tempor. Id eu sit consequat esse pariatur aliqua dolor tempor consequat sit aliquip. Labore et eu eu laboris amet velit amet ipsum ut aute aute magna nostrud.\r\n",
          "registered": "2017-11-05T10:06:55 -01:00",
          "salary": {
            "month": 3942,
            "bonus": 2665
          }
        },
        {
          "_id": "5d8ca4d39a647b56f7720efe",
          "isActive": true,
          "balance": "$2,423.44",
          "age": 40,
          "eyeColor": "brown",
          "lastname": " Clark",
          "firstname": "Vickie",
          "gender": "female",
          "company": "INRT",
          "email": "vickieclark@inrt.com",
          "phone": "+1 (957) 486-2370",
          "address": "783 Bank Street, Barronett, Connecticut, 7519",
          "about": "Consequat commodo elit veniam et ea duis. Quis id irure ipsum fugiat incididunt adipisicing tempor. Id id nostrud eu veniam aute. Aliqua elit do labore ex incididunt ea nulla in ea minim cupidatat exercitation dolore. Culpa esse ut deserunt nisi labore. Duis reprehenderit irure nulla voluptate reprehenderit adipisicing.\r\n",
          "registered": "2016-12-27T12:46:55 -01:00",
          "salary": {
            "month": 2645,
            "bonus": 2885
          }
        },
        {
          "_id": "5d8ca4d393237cb1bca13bbb",
          "isActive": false,
          "balance": "$2,338.54",
          "age": 32,
          "eyeColor": "brown",
          "lastname": " Mcconnell",
          "firstname": "Shields",
          "gender": "male",
          "company": "SUNCLIPSE",
          "email": "shieldsmcconnell@sunclipse.com",
          "phone": "+1 (930) 563-2967",
          "address": "768 National Drive, Tilden, California, 7026",
          "about": "Amet et velit laboris consectetur cillum id. Est nulla magna nisi velit consequat ad incididunt sint pariatur. Irure consequat aliqua irure sint minim velit culpa elit deserunt. Mollit commodo anim aute quis esse ea velit veniam. Amet in est cillum tempor id. Nostrud anim mollit laborum duis id quis nisi veniam.\r\n",
          "registered": "2015-07-29T03:49:21 -02:00",
          "salary": {
            "month": 3907,
            "bonus": 9424
          }
        },
        {
          "_id": "5d8ca4d3d46eeccd74b65ec0",
          "isActive": true,
          "balance": "$3,193.68",
          "age": 34,
          "eyeColor": "green",
          "lastname": " Ramos",
          "firstname": "Arnold",
          "gender": "male",
          "company": "COMSTAR",
          "email": "arnoldramos@comstar.com",
          "phone": "+1 (853) 417-3544",
          "address": "953 Brighton Court, Kersey, South Dakota, 3246",
          "about": "Labore minim magna duis cupidatat magna. Nostrud aute aliquip eu Lorem dolor sunt cupidatat Lorem nisi minim proident nisi quis pariatur. Est labore irure aliquip officia anim eiusmod eu. Sit cupidatat elit consequat esse nulla proident qui Lorem irure qui tempor.\r\n",
          "registered": "2017-09-10T03:41:40 -02:00",
          "salary": {
            "month": 2652,
            "bonus": 4960
          }
        },
        {
          "_id": "5d8ca4d31ca28c0cdf995167",
          "isActive": true,
          "balance": "$2,569.60",
          "age": 25,
          "eyeColor": "green",
          "lastname": " Mathews",
          "firstname": "Lora",
          "gender": "female",
          "company": "DIGIGEN",
          "email": "loramathews@digigen.com",
          "phone": "+1 (949) 472-3287",
          "address": "627 Preston Court, Chilton, Utah, 5686",
          "about": "Aliquip fugiat in est mollit non mollit sit officia irure ex labore dolor mollit. Proident velit ullamco ut eiusmod proident non consectetur enim irure aliqua. Proident tempor deserunt minim nisi deserunt Lorem ex. Officia ad amet nulla proident fugiat labore non. Enim pariatur irure commodo adipisicing tempor incididunt ad dolore quis id. Non magna in consectetur irure enim esse elit proident proident cillum sint culpa amet.\r\n",
          "registered": "2015-08-01T07:13:32 -02:00",
          "salary": {
            "month": 2560,
            "bonus": 4757
          }
        },
        {
          "_id": "5d8ca4d3ebfb66c8de537cfa",
          "isActive": true,
          "balance": "$1,485.05",
          "age": 36,
          "eyeColor": "blue",
          "lastname": " Hewitt",
          "firstname": "Hull",
          "gender": "male",
          "company": "INCUBUS",
          "email": "hullhewitt@incubus.com",
          "phone": "+1 (817) 529-3098",
          "address": "381 Loring Avenue, Abrams, Vermont, 4140",
          "about": "Velit ad voluptate officia id fugiat. Id enim esse tempor enim dolor in in. Nisi exercitation irure aliqua officia fugiat excepteur laborum aliqua quis exercitation.\r\n",
          "registered": "2015-05-15T05:18:50 -02:00",
          "salary": {
            "month": 1586,
            "bonus": 3117
          }
        },
        {
          "_id": "5d8ca4d35606fe8bd27fa315",
          "isActive": false,
          "balance": "$1,123.81",
          "age": 40,
          "eyeColor": "blue",
          "lastname": " Dalton",
          "firstname": "Bette",
          "gender": "female",
          "company": "ANIMALIA",
          "email": "bettedalton@animalia.com",
          "phone": "+1 (883) 404-3200",
          "address": "779 Graham Avenue, Healy, Ohio, 3496",
          "about": "Non est et consectetur ipsum dolore commodo pariatur ut pariatur enim excepteur eu sint. Do cillum do id velit sunt enim. Incididunt commodo excepteur veniam incididunt aute reprehenderit laborum aute. Ullamco velit fugiat est qui. Duis elit tempor sit Lorem tempor adipisicing enim quis. Fugiat sunt qui occaecat culpa commodo pariatur voluptate amet voluptate enim.\r\n",
          "registered": "2019-01-22T04:33:39 -01:00",
          "salary": {
            "month": 3496,
            "bonus": 1721
          }
        },
        {
          "_id": "5d8ca4d3e7f856e74ba8600f",
          "isActive": false,
          "balance": "$1,100.22",
          "age": 23,
          "eyeColor": "green",
          "lastname": " Dunlap",
          "firstname": "Wilson",
          "gender": "male",
          "company": "SHADEASE",
          "email": "wilsondunlap@shadease.com",
          "phone": "+1 (879) 450-3120",
          "address": "938 Carlton Avenue, Dotsero, Federated States Of Micronesia, 561",
          "about": "Reprehenderit excepteur ad sunt consectetur. Cupidatat labore duis reprehenderit in officia mollit laborum magna tempor. Voluptate amet adipisicing velit ea est. Ipsum voluptate sit eiusmod aute aliqua elit ex fugiat nulla consequat sunt voluptate anim id.\r\n",
          "registered": "2018-07-02T05:44:11 -02:00",
          "salary": {
            "month": 3536,
            "bonus": 2358
          }
        },
        {
          "_id": "5d8ca4d3ec9c661e84927d4d",
          "isActive": true,
          "balance": "$2,459.50",
          "age": 35,
          "eyeColor": "blue",
          "lastname": " Chen",
          "firstname": "Millicent",
          "gender": "female",
          "company": "DEEPENDS",
          "email": "millicentchen@deepends.com",
          "phone": "+1 (932) 505-3265",
          "address": "545 Monument Walk, Brecon, Maryland, 3460",
          "about": "Cillum esse occaecat pariatur non nulla anim commodo et esse nisi ad. Ad ullamco irure sunt sint. Do fugiat voluptate quis culpa aliqua Lorem labore consectetur et labore adipisicing. Ea proident commodo officia eiusmod non mollit enim cupidatat sit non.\r\n",
          "registered": "2014-01-11T03:01:07 -01:00",
          "salary": {
            "month": 2642,
            "bonus": 1831
          }
        },
        {
          "_id": "5d8ca4d3890f892b46567dee",
          "isActive": true,
          "balance": "$3,457.39",
          "age": 26,
          "eyeColor": "blue",
          "lastname": " Floyd",
          "firstname": "Shelby",
          "gender": "female",
          "company": "HANDSHAKE",
          "email": "shelbyfloyd@handshake.com",
          "phone": "+1 (890) 577-3207",
          "address": "471 Congress Street, Staples, Pennsylvania, 4126",
          "about": "Occaecat ad cupidatat nulla ea cupidatat nulla officia eu dolore reprehenderit culpa qui. Qui ullamco excepteur ullamco reprehenderit qui esse enim cillum aliqua fugiat. Irure Lorem proident deserunt laborum elit aliqua voluptate proident cupidatat. Dolor ex cupidatat esse aute aliqua Lorem reprehenderit consectetur mollit amet aliqua ex. Exercitation ea anim occaecat ut id nulla qui dolore laborum fugiat excepteur fugiat quis nostrud. Mollit mollit et reprehenderit id officia enim duis aliquip culpa ea. Fugiat officia incididunt deserunt proident labore culpa commodo consectetur nisi sunt minim velit.\r\n",
          "registered": "2016-08-26T01:52:37 -02:00",
          "salary": {
            "month": 1967,
            "bonus": 9492
          }
        }
      ],
      config: {
        cols: [
          {
            key: 'gender',
            label: 'Genre',
          },
          {
            label: 'Utilisateur',
            value: (line) => `${line.firstname} ${line.lastname}`,
            subCols: [
              {
                label: 'Prénom',
                value: 'firstname'
              },
              {
                label: 'Nom',
                value: 'lastname'
              },
              {
                label: 'Email',
                value: 'email'
              },
              {
                label: 'Détails',
                value: () => { return null; },
                subCols: [
                  {
                    label: 'Age',
                    value: 'age'
                  },
                  {
                    label: 'Tel',
                    value: 'phone'
                  }
                ]
              },
            ]
          },
          {
            label: 'Salaire',
            value: 'salary.month',
            subCols: [
              {
                label: 'Mensuel',
                value: 'salary.month'
              },
              {
                label: 'Bonus Annuel',
                value: 'salary.bonus'
              }
            ]
          },
          {
            label: 'Date début',
            value: 'registered',
          },
          {
            label: 'A propos',
            value: 'about',
          },
          {
            label: 'Entreprise',
            value: 'company',
          },
          {
            label: 'Adresse',
            value: 'address',
          },
        ]
      }
    }
  },
}
</script>

<style>
  /*.table {*/
  /*  display: table;*/

  /*}*/

  /*.row {*/
  /*  display: table-row;*/
  /*}*/

  /*.cell-unstyled {*/
  /*  display: table-cell;*/
  /*}*/

  /*.cell {*/
  /*  display: table-cell;*/
  /*  text-align: center;*/
  /*  padding: 10px;*/
  /*  border: 1px solid black;*/
  /*}*/
</style>