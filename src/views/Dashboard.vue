<template>
     <div > 
      <div class ="row">
            <div class="column">
                <h2>Banned Countries </h2>
            </div>
            <div class="column"> 
                <button type="button" class="btn btn-primary"> Back</button>
            </div>
      </div>
          <p>Banned</p>
          <div class="scroll" style="background-color: rgb(252, 252, 252); padding:10px ">  
               <span    v-for="(list, index) in country" 
                        v-bind:key="list.name"
                        v-if="list.isbanned" 
                        v-bind="country">  
                    <button  class="btn" style="padding:5px; margin:5px;font-size: small; background-color: rgb(203, 229, 240);" v-on:click="remove_country($event, list)"> {{ list.name}} <CButtonClose/> </button>
               </span>
          </div>

          <div>
               <p>Select Banned Countries</p>
               <input id="checkall" name="checkall" type="checkbox" v-on:change="selectall"  >
               <span > Select All </span>
          </div>
          
          <CButtonGroup variant="pills">
          <label    v-for="(doc , index) in group_list">
               <CButton style="padding:5px; margin:5px;"  v-on:click="select_part($event, doc)"> {{doc}}  </CButton> 
          </label>
          </CButtonGroup>
          <hr>

        <div  class="scroll_country" > 
          
          <ul v-for="(doc, index) in group_select" >

               <ul v-for="(grp, index) in [doc[0], doc[1], doc[2]]">
                    <br>
                    <lable> {{grp}} </lable>
                    <br>
                    <br>

                    <li  v-for="(list, index) in country"  v-if="list.name[0] == grp">

                         <input    type="checkbox" 
                                   v-on:change="update($event, list)" 
                                   v-bind:checked="list.isbanned"/>
                         <span> {{list.name}}</span>
                         
                    </li>
               </ul>
          </ul>

        </div>

        <br>
        <br>
        <div class ="row">
          <div class="column">
               <button type="button" class="btn btn-primary"> Back</button>
          </div>
          <div class="column"> 
               <button type="button" class="btn btn-primary"v-on:click="save_banned" > Save</button>
          </div>
     </div>

     </div>
</template>

<script>
// import MainChartExample from './charts/MainChartExample'
// import WidgetsDropdown from './widgets/WidgetsDropdown'
// import WidgetsBrand from './widgets/WidgetsBrand'

export default {
  name: 'Banned Countries',
  components: {
    // MainChartExample,
    // WidgetsDropdown,
    // WidgetsBrand
  },
  data () {
    return {
          select_all : false , 
          group_select : ['ABC', 'DEF','GHI', 'JKL', 'MN', 'OPQ', 'RST', 'UVW', 'XYZ'], 
          group_list : ['ABC', 'DEF','GHI', 'JKL', 'MN', 'OPQ', 'RST', 'UVW', 'XYZ'],
          group     : ['A','B', 'C', 'D','E','F', 'G','H','I', 'J','K','L', 'M','N', 'O','P','Q', 'R','S','T', 'U','V','W','X','Y','Z'],
          country   : [{id: 0, name: 'Afghanistan', isbanned: false}, 
          
          {id: 1, name: 'Aland Islands', isbanned: false}, 
          {id: 2, name: 'Albania', isbanned: false}, 
          {id: 3, name: 'Algeria', isbanned: false}, {id: 4, name: 'American Samoa', isbanned: false}, {id: 5, name: 'AndorrA', isbanned: false}, {id: 6, name: 'Angola', isbanned: false}, {id: 7, name: 'Anguilla', isbanned: false}, {id: 8, name: 'Antarctica', isbanned: false}, {id: 9, name: 'Antigua and Barbuda', isbanned: false}, {id: 10, name: 'Argentina', isbanned: false}, {id: 11, name: 'Armenia', isbanned: false}, {id: 12, name: 'Aruba', isbanned: false}, {id: 13, name: 'Australia', isbanned: false}, {id: 14, name: 'Austria', isbanned: false}, {id: 15, name: 'Azerbaijan', isbanned: false}, {id: 16, name: 'Bahamas', isbanned: false}, {id: 17, name: 'Bahrain', isbanned: false}, {id: 18, name: 'Bangladesh', isbanned: false}, {id: 19, name: 'Barbados', isbanned: false}, {id: 20, name: 'Belarus', isbanned: false}, {id: 21, name: 'Belgium', isbanned: false}, {id: 22, name: 'Belize', isbanned: false}, {id: 23, name: 'Benin', isbanned: false}, {id: 24, name: 'Bermuda', isbanned: false}, {id: 25, name: 'Bhutan', isbanned: false}, {id: 26, name: 'Bolivia', isbanned: false}, {id: 27, name: 'Bosnia and Herzegovina', isbanned: false}, {id: 28, name: 'Botswana', isbanned: false}, {id: 29, name: 'Bouvet Island', isbanned: false}, {id: 30, name: 'Brazil', isbanned: false}, {id: 31, name: 'British Indian Ocean Territory', isbanned: false}, {id: 32, name: 'Brunei Darussalam', isbanned: false}, {id: 33, name: 'Bulgaria', isbanned: false}, {id: 34, name: 'Burkina Faso', isbanned: false}, {id: 35, name: 'Burundi', isbanned: false}, {id: 36, name: 'Cambodia', isbanned: false}, {id: 37, name: 'Cameroon', isbanned: false}, {id: 38, name: 'Canada', isbanned: false}, {id: 39, name: 'Cape Verde', isbanned: false}, {id: 40, name: 'Cayman Islands', isbanned: false}, {id: 41, name: 'Central African Republic', isbanned: false}, {id: 42, name: 'Chad', isbanned: false}, {id: 43, name: 'Chile', isbanned: false}, {id: 44, name: 'China', isbanned: false}, {id: 45, name: 'Christmas Island', isbanned: false}, {id: 46, name: 'Cocos (Keeling) Islands', isbanned: false}, {id: 47, name: 'Colombia', isbanned: false}, {id: 48, name: 'Comoros', isbanned: false}, {id: 49, name: 'Congo', isbanned: false}, {id: 50, name: 'Congo, The Democratic Republic of the', isbanned: false}, {id: 51, name: 'Cook Islands', isbanned: false}, {id: 52, name: 'Costa Rica', isbanned: false}, {id: 53, name: "Cote DIvoire", isbanned: false}, {id: 54, name: 'Croatia', isbanned: false}, {id: 55, name: 'Cuba', isbanned: false}, {id: 56, name: 'Cyprus', isbanned: false}, {id: 57, name: 'Czech Republic', isbanned: false}, {id: 58, name: 'Denmark', isbanned: false}, {id: 59, name: 'Djibouti', isbanned: false}, {id: 60, name: 'Dominica', isbanned: false}, {id: 61, name: 'Dominican Republic', isbanned: false}, {id: 62, name: 'Ecuador', isbanned: false}, {id: 63, name: 'Egypt', isbanned: false}, {id: 64, name: 'El Salvador', isbanned: false}, {id: 65, name: 'Equatorial Guinea', isbanned: false}, {id: 66, name: 'Eritrea', isbanned: false}, {id: 67, name: 'Estonia', isbanned: false}, {id: 68, name: 'Ethiopia', isbanned: false}, {id: 69, name: 'Falkland Islands (Malvinas)', isbanned: false}, {id: 70, name: 'Faroe Islands', isbanned: false}, {id: 71, name: 'Fiji', isbanned: false}, {id: 72, name: 'Finland', isbanned: false}, {id: 73, name: 'France', isbanned: false}, {id: 74, name: 'French Guiana', isbanned: false}, {id: 75, name: 'French Polynesia', isbanned: false}, {id: 76, name: 'French Southern Territories', isbanned: false}, {id: 77, name: 'Gabon', isbanned: false}, {id: 78, name: 'Gambia', isbanned: false}, {id: 79, name: 'Georgia', isbanned: false}, {id: 80, name: 'Germany', isbanned: false}, {id: 81, name: 'Ghana', isbanned: false}, {id: 82, name: 'Gibraltar', isbanned: false}, {id: 83, name: 'Greece', isbanned: false}, {id: 84, name: 'Greenland', isbanned: false}, {id: 85, name: 'Grenada', isbanned: false}, {id: 86, name: 'Guadeloupe', isbanned: false}, {id: 87, name: 'Guam', isbanned: false}, {id: 88, name: 'Guatemala', isbanned: false}, {id: 89, name: 'Guernsey', isbanned: false}, {id: 90, name: 'Guinea', isbanned: false}, {id: 91, name: 'Guinea-Bissau', isbanned: false}, {id: 92, name: 'Guyana', isbanned: false}, {id: 93, name: 'Haiti', isbanned: false}, {id: 94, name: 'Heard Island and Mcdonald Islands', isbanned: false}, {id: 95, name: 'Holy See (Vatican City State)', isbanned: false}, {id: 96, name: 'Honduras', isbanned: false}, {id: 97, name: 'Hong Kong', isbanned: false}, {id: 98, name: 'Hungary', isbanned: false}, {id: 99, name: 'Iceland', isbanned: false}, {id: 100, name: 'India', isbanned: false}, {id: 101, name: 'Indonesia', isbanned: false}, {id: 102, name: 'Iran, Islamic Republic Of', isbanned: false}, {id: 103, name: 'Iraq', isbanned: false}, {id: 104, name: 'Ireland', isbanned: false}, {id: 105, name: 'Isle of Man', isbanned: false}, {id: 106, name: 'Israel', isbanned: false}, {id: 107, name: 'Italy', isbanned: false}, {id: 108, name: 'Jamaica', isbanned: false}, {id: 109, name: 'Japan', isbanned: false}, {id: 110, name: 'Jersey', isbanned: false}, {id: 111, name: 'Jordan', isbanned: false}, {id: 112, name: 'Kazakhstan', isbanned: false}, {id: 113, name: 'Kenya', isbanned: false}, {id: 114, name: 'Kiribati', isbanned: false}, {id: 115, name: "Korea, Democratic PeopleS Republic of", isbanned: false}, {id: 116, name: 'Korea, Republic of', isbanned: false}, {id: 117, name: 'Kuwait', isbanned: false}, {id: 118, name: 'Kyrgyzstan', isbanned: false}, {id: 119, name: "Lao PeopleS Democratic Republic", isbanned: false}, {id: 120, name: 'Latvia', isbanned: false}, {id: 121, name: 'Lebanon', isbanned: false}, {id: 122, name: 'Lesotho', isbanned: false}, {id: 123, name: 'Liberia', isbanned: false}, {id: 124, name: 'Libyan Arab Jamahiriya', isbanned: false}, {id: 125, name: 'Liechtenstein', isbanned: false}, {id: 126, name: 'Lithuania', isbanned: false}, {id: 127, name: 'Luxembourg', isbanned: false}, {id: 128, name: 'Macao', isbanned: false}, {id: 129, name: 'Macedonia, The Former Yugoslav Republic of', isbanned: false}, {id: 130, name: 'Madagascar', isbanned: false}, {id: 131, name: 'Malawi', isbanned: false}, {id: 132, name: 'Malaysia', isbanned: false}, {id: 133, name: 'Maldives', isbanned: false}, {id: 134, name: 'Mali', isbanned: false}, {id: 135, name: 'Malta', isbanned: false}, {id: 136, name: 'Marshall Islands', isbanned: false}, {id: 137, name: 'Martinique', isbanned: false}, {id: 138, name: 'Mauritania', isbanned: false}, {id: 139, name: 'Mauritius', isbanned: false}, {id: 140, name: 'Mayotte', isbanned: false}, {id: 141, name: 'Mexico', isbanned: false}, {id: 142, name: 'Micronesia, Federated States of', isbanned: false}, {id: 143, name: 'Moldova, Republic of', isbanned: false}, {id: 144, name: 'Monaco', isbanned: false}, {id: 145, name: 'Mongolia', isbanned: false}, {id: 146, name: 'Montserrat', isbanned: false}, {id: 147, name: 'Morocco', isbanned: false}, {id: 148, name: 'Mozambique', isbanned: false}, {id: 149, name: 'Myanmar', isbanned: false}, {id: 150, name: 'Namibia', isbanned: false}, {id: 151, name: 'Nauru', isbanned: false}, {id: 152, name: 'Nepal', isbanned: false}, {id: 153, name: 'Netherlands', isbanned: false}, {id: 154, name: 'Netherlands Antilles', isbanned: false}, {id: 155, name: 'New Caledonia', isbanned: false}, {id: 156, name: 'New Zealand', isbanned: false}, {id: 157, name: 'Nicaragua', isbanned: false}, {id: 158, name: 'Niger', isbanned: false}, {id: 159, name: 'Nigeria', isbanned: false}, {id: 160, name: 'Niue', isbanned: false}, {id: 161, name: 'Norfolk Island', isbanned: false}, {id: 162, name: 'Northern Mariana Islands', isbanned: false}, {id: 163, name: 'Norway', isbanned: false}, {id: 164, name: 'Oman', isbanned: false}, {id: 165, name: 'Pakistan', isbanned: false}, {id: 166, name: 'Palau', isbanned: false}, {id: 167, name: 'Palestinian Territory, Occupied', isbanned: false}, {id: 168, name: 'Panama', isbanned: false}, {id: 169, name: 'Papua New Guinea', isbanned: false}, {id: 170, name: 'Paraguay', isbanned: false}, {id: 171, name: 'Peru', isbanned: false}, {id: 172, name: 'Philippines', isbanned: false}, {id: 173, name: 'Pitcairn', isbanned: false}, {id: 174, name: 'Poland', isbanned: false}, {id: 175, name: 'Portugal', isbanned: false}, {id: 176, name: 'Puerto Rico', isbanned: false}, {id: 177, name: 'Qatar', isbanned: false}, {id: 178, name: 'Reunion', isbanned: false}, {id: 179, name: 'Romania', isbanned: false}, {id: 180, name: 'Russian Federation', isbanned: false}, {id: 181, name: 'RWANDA', isbanned: false}, {id: 182, name: 'Saint Helena', isbanned: false}, {id: 183, name: 'Saint Kitts and Nevis', isbanned: false}, {id: 184, name: 'Saint Lucia', isbanned: false}, {id: 185, name: 'Saint Pierre and Miquelon', isbanned: false}, {id: 186, name: 'Saint Vincent and the Grenadines', isbanned: false}, {id: 187, name: 'Samoa', isbanned: false}, {id: 188, name: 'San Marino', isbanned: false}, {id: 189, name: 'Sao Tome and Principe', isbanned: false}, {id: 190, name: 'Saudi Arabia', isbanned: false}, {id: 191, name: 'Senegal', isbanned: false}, {id: 192, name: 'Serbia and Montenegro', isbanned: false}, {id: 193, name: 'Seychelles', isbanned: false}, {id: 194, name: 'Sierra Leone', isbanned: false}, {id: 195, name: 'Singapore', isbanned: false}, {id: 196, name: 'Slovakia', isbanned: false}, {id: 197, name: 'Slovenia', isbanned: false}, {id: 198, name: 'Solomon Islands', isbanned: false}, {id: 199, name: 'Somalia', isbanned: false}, {id: 200, name: 'South Africa', isbanned: false}, {id: 201, name: 'South Georgia and the South Sandwich Islands', isbanned: false}, {id: 202, name: 'Spain', isbanned: false}, {id: 203, name: 'Sri Lanka', isbanned: false}, {id: 204, name: 'Sudan', isbanned: false}, {id: 205, name: 'Suri', isbanned: false}, {id: 206, name: 'Svalbard and Jan Mayen', isbanned: false}, {id: 207, name: 'Swaziland', isbanned: false}, {id: 208, name: 'Sweden', isbanned: false}, {id: 209, name: 'Switzerland', isbanned: false}, {id: 210, name: 'Syrian Arab Republic', isbanned: false}, {id: 211, name: 'Taiwan, Province of China', isbanned: false}, {id: 212, name: 'Tajikistan', isbanned: false}, {id: 213, name: 'Tanzania, United Republic of', isbanned: false}, {id: 214, name: 'Thailand', isbanned: false}, {id: 215, name: 'Timor-Leste', isbanned: false}, {id: 216, name: 'Togo', isbanned: false}, {id: 217, name: 'Tokelau', isbanned: false}, {id: 218, name: 'Tonga', isbanned: false}, {id: 219, name: 'Trinidad and Tobago', isbanned: false}, {id: 220, name: 'Tunisia', isbanned: false}, {id: 221, name: 'Turkey', isbanned: false}, {id: 222, name: 'Turkmenistan', isbanned: false}, {id: 223, name: 'Turks and Caicos Islands', isbanned: false}, {id: 224, name: 'Tuvalu', isbanned: false}, {id: 225, name: 'Uganda', isbanned: false}, {id: 226, name: 'Ukraine', isbanned: false}, {id: 227, name: 'United Arab Emirates', isbanned: false}, {id: 228, name: 'United Kingdom', isbanned: false}, {id: 229, name: 'United States', isbanned: false}, {id: 230, name: 'United States Minor Outlying Islands', isbanned: false}, {id: 231, name: 'Uruguay', isbanned: false}, {id: 232, name: 'Uzbekistan', isbanned: false}, {id: 233, name: 'Vanuatu', isbanned: false}, {id: 234, name: 'Venezuela', isbanned: false}, {id: 235, name: 'Viet Nam', isbanned: false}, {id: 236, name: 'Virgin Islands, British', isbanned: false}, {id: 237, name: 'Virgin Islands, U.S.', isbanned: false}, {id: 238, name: 'Wallis and Futuna', isbanned: false}, {id: 239, name: 'Western Sahara', isbanned: false}, {id: 240, name: 'Yemen', isbanned: false}, {id: 241, name: 'Zambia', isbanned: false}, {id: 242, name: 'Zimbabwe', isbanned: false}]
          
     }},
     methods : {

               update: function (e, list) {

                    console.log(list.name + list.id + list.isbanned)
                    list.isbanned =!list.isbanned
                    console.log(list.isbanned)

               },
               selectall: function (e) {

                      if (e.target.checked) {

                        for(let doc of this.country){
                          doc.isbanned = true 
                        }

                      } else {

                        for(let doc of this.country){
                          doc.isbanned = false 
                      }     
                      }   
                                      
  
               },
               remove_country: function (e, list) {
                         list.isbanned = !list.isbanned 
               },
               select_part: function (e, list) {

                    this.group_select =  [list]
                    // alert(list)
               },               
               save_banned: function (e, list) {
                    var banned_list =[]
                    // banned_list.attribute.push({})

                    for (let doc of this.country) {

                         

                         if(doc.isbanned) {

                            const str ="{'name':'"+ doc.name + "'}"

                            banned_list.push(str)

                          }


                         
                         
                    }

                    	let file = banned_list
                      let filename = 'banned_list.json'
                      let element = document.createElement('a')
                      element.setAttribute('href', 'data:application/json;charset=utf-8,' +encodeURIComponent(file))
                      element.setAttribute('download', filename)
                      element.style.display = 'none'
                      document.body.appendChild(element)
                      element.click()
                      document.body.removeChild(element)

                    
    }     
     
  }

}
  

</script>

     <style>
          div.scroll {
            width: 95%;
            height: 100px;
            overflow: auto;
            overflow-y: scroll;
            text-align: justify;
            padding: 20px;
            font: small;
            font-family: Arial;
          }
          div.scroll_country {
            width: 95%;
            height: 208px;
            overflow-y: auto;
            text-align: justify;
            padding: 20px;
            font-size: small;
            font-family: Arial;
            background-color: rgb(252, 252, 252);

          }
     ul {
     float: left;
     width: 100%;
     margin: 0;
     padding: 0;
     list-style: none;
     }

     li {
     float: left;
     width: 25%;
     margin: 0;
     padding: 0;
     } 

     * {
       font-family: Arial;
     }
     
.column {
  float: left;
  width: 50%;
}
.row:after {
  content: "";
  display: table;
  clear: both;
}



  </style>
