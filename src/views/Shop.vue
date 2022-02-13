<template>
  <v-container>
    <h1>Shop Page</h1>

    <v-container class="d-flex flex-wrap">
      <v-card
        class="mx-auto mb-5"
        max-width="344"
        v-for="(product, index) in productList"
        :key="index"
      >
        <v-img :src="product.image" height="200px"></v-img>

        <v-card-title> {{ product.id }}.{{ product.title }} </v-card-title>

        <v-card-subtitle
          >{{ product.price }} $ <v-spacer></v-spacer>
          <v-rating
            :value="product.rating.rate"
            color="amber"
            dense
            half-increments
            readonly
            size="14"
          ></v-rating>
          <div class="grey--text ms-4">{{ product.rating.count }}</div>
        </v-card-subtitle>

        <v-card-actions>
          <v-btn
            color="green accent-2"
            text
            :to="{
              name: 'detail',
              params: { id: product.id, description: product.description },
            }"
          >
            รายละเอียด
          </v-btn>
          <div>
            <button class="btn btn-success" @click="addCart(product)">
              Add to Cart
            </button>
          </div>

          <v-spacer></v-spacer>

          <v-btn icon @click="show = !show">
            <v-icon>{{ show ? "mdi-chevron-up" : "mdi-chevron-down" }}</v-icon>
          </v-btn>
        </v-card-actions>

        <v-expand-transition>
          <div v-show="show">
            <hr>
            <v-card-text> category : {{ product.category }} </v-card-text>
          </div>
        </v-expand-transition>
      </v-card>
      <v-container>
        <v-card>
          <div class="container col-md-12" v-if="carts != 0">
            <h4>Cart</h4>
            <hr>
            <table class="table">
              <thead>
                <tr>
                  <th scope="col">รหัสสินค้า</th>
                  <th scope="col">ภาพสินค้า</th>
                  <th scope="col">ชื่อ</th>
                  <th scope="col">ราคา</th>
                  <th scope="col">จำนวน</th>
                  <th scope="col">ยอดรวม</th>
                  <th scope="col">ลบ</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="(item, index) in carts" :key="index">
                  <td>{{ item.id }}</td>
                  <td><img :src="item.image" height="50px" width="50px" /></td>
                  <td>{{ item.name }}</td>
                  <td>{{ item.price }} $</td>
                  <td>
                    {{ item.qty }}
                    <i class="fa fa-plus qty-plus" @click="plusqty(item)"></i>
                    <i class="fa fa-minus qty-minus" @click="minusqty(item)"></i>
                  </td>
                  <td>{{ item.total }} $</td>
                  <td>
                    <button @click="removeproduct(item)" class="btn-Success">
                      <i class="fa fa-trash"></i>
                    </button>
                  </td>
                </tr>
              </tbody>
            </table>

            <v-card-footer>
              <center>
                <h3>PAY : {{ total() }} $</h3>
              </center>
            </v-card-footer>
          </div>
        </v-card>
      </v-container>
      <v-container grid-list-xs class="green accent-2">
        <router-view :key="$route.path"></router-view>
      </v-container>
    </v-container>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      carts: [],
      c1: 0,
      c2: 0,
      c3: 0,
      c4: 0,
      c5: 0,
      c6: 0,
      c7: 0,
      c8: 0,
      c9: 0,
      c10: 0,
      c11: 0,
      c12: 0,
      c13: 0,
      c14: 0,
      c15: 0,
      c16: 0,
      c17: 0,
      c18: 0,
      c19: 0,
      c20: 0,
      show: false,
      productList: [
        {
          id: 1,
          title: "Fjallraven - Foldsack No. 1 Backpack, Fits 15 Laptops",
          price: 110,
          description:
            "Your perfect pack for everyday use and walks in the forest. Stash your laptop (up to 15 inches) in the padded sleeve, your everyday",
          category: "men's clothing",
          image: "https://fakestoreapi.com/img/81fPKd-2AYL._AC_SL1500_.jpg",

          rating: {
            rate: 3.9,
            count: 120,
          },
          active: false,
        },

        {
          id: 2,
          title: "Mens Casual Premium Slim Fit T-Shirts ",
          price: 23,
          description:
            "Slim-fitting style, contrast raglan long sleeve, three-button henley placket, light weight & soft fabric for breathable and comfortable wearing. And Solid stitched shirts with round neck made for durability and a great fit for casual fashion wear and diehard baseball fans. The Henley style round neckline includes a three-button placket.",
          category: "men's clothing",
          image:
            "https://fakestoreapi.com/img/71-3HjGNDUL._AC_SY879._SX._UX._SY._UY_.jpg",

          rating: {
            rate: 4.1,
            count: 259,
          },
          active: false,
        },

        {
          id: 3,
          title: "Mens Cotton Jacket",
          price: 56,
          description:
            "great outerwear jackets for Spring/Autumn/Winter, suitable for many occasions, such as working, hiking, camping, mountain/rock climbing, cycling, traveling or other outdoors. Good gift choice for you or your family member. A warm hearted love to Father, husband or son in this thanksgiving or Christmas Day.",
          category: "men's clothing",
          image: "https://fakestoreapi.com/img/71li-ujtlUL._AC_UX679_.jpg",

          rating: {
            rate: 4.7,
            count: 500,
          },
          active: false,
        },

        {
          id: 4,
          title: "Mens Casual Slim Fit",
          price: 16,
          description:
            "The color could be slightly different between on the screen and in practice. / Please note that body builds vary by person, therefore, detailed size information should be reviewed below on the product description.",
          category: "men's clothing",
          image: "https://fakestoreapi.com/img/71YXzeOuslL._AC_UY879_.jpg",

          rating: {
            rate: 2.1,
            count: 430,
          },
          active: false,
        },

        {
          id: 5,
          title:
            "John Hardy Women's Legends Naga Gold & Silver Dragon Station Chain Bracelet",
          price: 695,
          description:
            "From our Legends Collection, the Naga was inspired by the mythical water dragon that protects the ocean's pearl. Wear facing inward to be bestowed with love and abundance, or outward for protection.",
          category: "jewelery",
          image:
            "https://fakestoreapi.com/img/71pWzhdJNwL._AC_UL640_QL65_ML3_.jpg",

          rating: {
            rate: 4.6,
            count: 400,
          },
          active: false,
        },

        {
          id: 6,
          title: "Solid Gold Petite Micropave ",
          price: 168,
          description:
            "Satisfaction Guaranteed. Return or exchange any order within 30 days.Designed and sold by Hafeez Center in the United States. Satisfaction Guaranteed. Return or exchange any order within 30 days.",
          category: "jewelery",
          image:
            "https://fakestoreapi.com/img/61sbMiUnoGL._AC_UL640_QL65_ML3_.jpg",

          rating: {
            rate: 3.9,
            count: 70,
          },
          active: false,
        },

        {
          id: 7,
          title: "White Gold Plated Princess",
          price: 10,
          description:
            "Classic Created Wedding Engagement Solitaire Diamond Promise Ring for Her. Gifts to spoil your love more for Engagement, Wedding, Anniversary, Valentine's Day...",
          category: "jewelery",
          image:
            "https://fakestoreapi.com/img/71YAIFU48IL._AC_UL640_QL65_ML3_.jpg",

          rating: {
            rate: 3,
            count: 400,
          },
          active: false,
        },

        {
          id: 8,
          title: "Pierced Owl Rose Gold Plated Stainless Steel Double",
          price: 11,
          description:
            "Rose Gold Plated Double Flared Tunnel Plug Earrings. Made of 316L Stainless Steel",
          category: "jewelery",
          image:
            "https://fakestoreapi.com/img/51UDEzMJVpL._AC_UL640_QL65_ML3_.jpg",

          rating: {
            rate: 1.9,
            count: 100,
          },
          active: false,
        },

        {
          id: 9,
          title: "WD 2TB Elements Portable External Hard Drive - USB 3.0 ",
          price: 64,
          description:
            "USB 3.0 and USB 2.0 Compatibility Fast data transfers Improve PC Performance High Capacity; Compatibility Formatted NTFS for Windows 10, Windows 8.1, Windows 7; Reformatting may be required for other operating systems; Compatibility may vary depending on user’s hardware configuration and operating system",
          category: "electronics",
          image: "https://fakestoreapi.com/img/61IBBVJvSDL._AC_SY879_.jpg",

          rating: {
            rate: 3.3,
            count: 203,
          },
          active: false,
        },

        {
          id: 10,
          title: "SanDisk SSD PLUS 1TB Internal SSD - SATA III 6 Gb/s",
          price: 109,
          description:
            "Easy upgrade for faster boot up, shutdown, application load and response (As compared to 5400 RPM SATA 2.5” hard drive; Based on published specifications and internal benchmarking tests using PCMark vantage scores) Boosts burst write performance, making it ideal for typical PC workloads The perfect balance of performance and reliability Read/write speeds of up to 535MB/s/450MB/s (Based on internal testing; Performance may vary depending upon drive capacity, host device, OS and application.)",
          category: "electronics",
          image: "https://fakestoreapi.com/img/61U7T1koQqL._AC_SX679_.jpg",

          rating: {
            rate: 2.9,
            count: 470,
          },
          active: false,
        },

        {
          id: 11,
          title:
            "Silicon Power 256GB SSD 3D NAND A55 SLC Cache Performance Boost SATA III 2.5",
          price: 109,
          description:
            "3D NAND flash are applied to deliver high transfer speeds Remarkable transfer speeds that enable faster bootup and improved overall system performance. The advanced SLC Cache Technology allows performance boost and longer lifespan 7mm slim design suitable for Ultrabooks and Ultra-slim notebooks. Supports TRIM command, Garbage Collection technology, RAID, and ECC (Error Checking & Correction) to provide the optimized performance and enhanced reliability.",
          category: "electronics",
          image: "https://fakestoreapi.com/img/71kWymZ+c+L._AC_SX679_.jpg",

          rating: {
            rate: 4.8,
            count: 319,
          },
          active: false,
        },

        {
          id: 12,
          title:
            "WD 4TB Gaming Drive Works with Playstation 4 Portable External Hard Drive",
          price: 114,
          description:
            "Expand your PS4 gaming experience, Play anywhere Fast and easy, setup Sleek design with high capacity, 3-year manufacturer's limited warranty",
          category: "electronics",
          image: "https://fakestoreapi.com/img/61mtL65D4cL._AC_SX679_.jpg",

          rating: {
            rate: 4.8,
            count: 400,
          },
          active: false,
        },

        {
          id: 13,
          title:
            "Acer SB220Q bi 21.5 inches Full HD (1920 x 1080) IPS Ultra-Thin",
          price: 599,
          description:
            "21. 5 inches Full HD (1920 x 1080) widescreen IPS display And Radeon free Sync technology. No compatibility for VESA Mount Refresh Rate: 75Hz - Using HDMI port Zero-frame design | ultra-thin | 4ms response time | IPS panel Aspect ratio - 16: 9. Color Supported - 16. 7 million colors. Brightness - 250 nit Tilt angle -5 degree to 15 degree. Horizontal viewing angle-178 degree. Vertical viewing angle-178 degree 75 hertz",
          category: "electronics",
          image: "https://fakestoreapi.com/img/81QpkIctqPL._AC_SX679_.jpg",

          rating: {
            rate: 2.9,
            count: 250,
          },
          active: false,
        },

        {
          id: 14,
          title:
            "Samsung 49-Inch CHG90 144Hz Curved Gaming Monitor (LC49HG90DMNXZA) – Super Ultrawide Screen QLED ",
          price: 1000,
          description:
            "49 INCH SUPER ULTRAWIDE 32:9 CURVED GAMING MONITOR with dual 27 inch screen side by side QUANTUM DOT (QLED) TECHNOLOGY, HDR support and factory calibration provides stunningly realistic and accurate color and contrast 144HZ HIGH REFRESH RATE and 1ms ultra fast response time work to eliminate motion blur, ghosting, and reduce input lag",
          category: "electronics",
          image: "https://fakestoreapi.com/img/81Zt42ioCgL._AC_SX679_.jpg",

          rating: {
            rate: 2.2,
            count: 140,
          },
          active: false,
        },

        {
          id: 15,
          title: "BIYLACLESEN Women's 3-in-1 Snowboard Jacket Winter Coats",
          price: 57,
          description:
            "Note:The Jackets is US standard size, Please choose size as your usual wear Material: 100% Polyester; Detachable Liner Fabric: Warm Fleece. Detachable Functional Liner: Skin Friendly, Lightweigt and Warm.Stand Collar Liner jacket, keep you warm in cold weather. Zippered Pockets: 2 Zippered Hand Pockets, 2 Zippered Pockets on Chest (enough to keep cards or keys)and 1 Hidden Pocket Inside.Zippered Hand Pockets and Hidden Pocket keep your things secure. Humanized Design: Adjustable and Detachable Hood and Adjustable cuff to prevent the wind and water,for a comfortable fit. 3 in 1 Detachable Design provide more convenience, you can separate the coat and inner as needed, or wear it together. It is suitable for different season and help you adapt to different climates",
          category: "women's clothing",
          image: "https://fakestoreapi.com/img/51Y5NI-I5jL._AC_UX679_.jpg",

          rating: {
            rate: 2.6,
            count: 235,
          },
          active: false,
        },

        {
          id: 16,
          title:
            "Lock and Love Women's Removable Hooded Faux Leather Moto Biker Jacket",
          price: 30,
          description:
            "100% POLYURETHANE(shell) 100% POLYESTER(lining) 75% POLYESTER 25% COTTON (SWEATER), Faux leather material for style and comfort / 2 pockets of front, 2-For-One Hooded denim style faux leather jacket, Button detail on waist / Detail stitching at sides, HAND WASH ONLY / DO NOT BLEACH / LINE DRY / DO NOT IRON",
          category: "women's clothing",
          image: "https://fakestoreapi.com/img/81XH0e8fefL._AC_UY879_.jpg",

          rating: {
            rate: 2.9,
            count: 340,
          },
          active: false,
        },

        {
          id: 17,
          title: "Rain Jacket Women Windbreaker Striped Climbing Raincoats",
          price: 40,
          description:
            "Lightweight perfet for trip or casual wear---Long sleeve with hooded, adjustable drawstring waist design. Button and zipper front closure raincoat, fully stripes Lined and The Raincoat has 2 side pockets are a good size to hold all kinds of things, it covers the hips, and the hood is generous but doesn't overdo it.Attached Cotton Lined Hood with Adjustable Drawstrings give it a real styled look.",
          category: "women's clothing",
          image: "https://fakestoreapi.com/img/71HblAHs5xL._AC_UY879_-2.jpg",

          rating: {
            rate: 3.8,
            count: 679,
          },
          active: false,
        },

        {
          id: 18,
          title: "MBJ Women's Solid Short Sleeve Boat Neck V ",
          price: 10,
          description:
            "95% RAYON 5% SPANDEX, Made in USA or Imported, Do Not Bleach, Lightweight fabric with great stretch for comfort, Ribbed on sleeves and neckline / Double stitching on bottom hem",
          category: "women's clothing",
          image: "https://fakestoreapi.com/img/71z3kpMAYsL._AC_UY879_.jpg",

          rating: {
            rate: 4.7,
            count: 130,
          },
          active: false,
        },

        {
          id: 19,
          title: "Opna Women's Short Sleeve Moisture",
          price: 8,
          description:
            "100% Polyester, Machine wash, 100% cationic polyester interlock, Machine Wash & Pre Shrunk for a Great Fit, Lightweight, roomy and highly breathable with moisture wicking fabric which helps to keep moisture away, Soft Lightweight Fabric with comfortable V-neck collar and a slimmer fit, delivers a sleek, more feminine silhouette and Added Comfort",
          category: "women's clothing",
          image: "https://fakestoreapi.com/img/51eg55uWmdL._AC_UX679_.jpg",

          rating: {
            rate: 4.5,
            count: 146,
          },
          active: false,
        },

        {
          id: 20,
          title: "DANVOUY Womens T Shirt Casual Cotton Short",
          price: 13,
          description:
            "95%Cotton,5%Spandex, Features: Casual, Short Sleeve, Letter Print,V-Neck,Fashion Tees, The fabric is soft and has some stretch., Occasion: Casual/Office/Beach/School/Home/Street. Season: Spring,Summer,Autumn,Winter.",
          category: "women's clothing",
          image: "https://fakestoreapi.com/img/61pHAEJ4NML._AC_UX679_.jpg",

          rating: {
            rate: 3.6,
            count: 145,
          },
          active: false,
        },
      ],
    };
  },
  methods: {
    addCart: function (product) {
      if (product.id == 1) {
        this.c1 += 1;
        if (this.c1 <= 1) {
          this.pushdata(product);
        } else {
          var cat1 = this.findindex(product);
          this.carts[cat1].qty += 1;
          this.carts[cat1].total = this.carts[cat1].qty * this.carts[cat1].price;
        }
      }
      if (product.id == 2) {
        this.c2 += 1;
        if (this.c2 <= 1) {
          this.pushdata(product);
        } else {
          var cat2 = this.findindex(product);
          this.carts[cat2].qty += 1;
          this.carts[cat2].total = this.carts[cat2].qty * this.carts[cat2].price;
        }
      }
      if (product.id == 3) {
        this.c3 += 1;
        if (this.c3 <= 1) {
          this.pushdata(product);
        } else {
          var cat3 = this.findindex(product);
          this.carts[cat3].qty += 1;
          this.carts[cat3].total = this.carts[cat3].qty * this.carts[cat3].price;
        }
      }
      if (product.id == 4) {
        this.c4 += 1;
        if (this.c4 <= 1) {
          this.pushdata(product);
        } else {
          var cat4 = this.findindex(product);
          this.carts[cat4].qty += 1;
          this.carts[cat4].total = this.carts[cat4].qty * this.carts[cat4].price;
        }
      }
      if (product.id == 5) {
        this.c5 += 1;
        if (this.c5 <= 1) {
          this.pushdata(product);
        } else {
          var cat5 = this.findindex(product);
          this.carts[cat5].qty += 1;
          this.carts[cat5].total = this.carts[cat5].qty * this.carts[cat5].price;
        }
      }
      if (product.id == 6) {
        this.c6 += 1;
        if (this.c6 <= 1) {
          this.pushdata(product);
        } else {
          var cat6 = this.findindex(product);
          this.carts[cat6].qty += 1;
          this.carts[cat6].total = this.carts[cat6].qty * this.carts[cat6].price;
        }
      }
      if (product.id == 7) {
        this.c7 += 1;
        if (this.c7 <= 1) {
          this.pushdata(product);
        } else {
          var cat7 = this.findindex(product);
          this.carts[cat7].qty += 1;
          this.carts[cat7].total = this.carts[cat7].qty * this.carts[cat7].price;
        }
      }
      if (product.id == 8) {
        this.c8 += 1;
        if (this.c8 <= 1) {
          this.pushdata(product);
        } else {
          var cat8 = this.findindex(product);
          this.carts[cat8].qty += 1;
          this.carts[cat8].total = this.carts[cat8].qty * this.carts[cat8].price;
        }
      }
      if (product.id == 9) {
        this.c9 += 1;
        if (this.c9 <= 1) {
          this.pushdata(product);
        } else {
          var cat9 = this.findindex(product);
          this.carts[cat9].qty += 1;
          this.carts[cat9].total = this.carts[cat9].qty * this.carts[cat9].price;
        }
      }
      if (product.id == 10) {
        this.c10 += 1;
        if (this.c10 <= 1) {
          this.pushdata(product);
        } else {
          var cat10 = this.findindex(product);
          this.carts[cat10].qty += 1;
          this.carts[cat10].total = this.carts[cat10].qty * this.carts[cat10].price;
        }
      }
      if (product.id == 11) {
        this.c11 += 1;
        if (this.c11 <= 1) {
          this.pushdata(product);
        } else {
          var cat11 = this.findindex(product);
          this.carts[cat11].qty += 1;
          this.carts[cat11].total = this.carts[cat11].qty * this.carts[cat11].price;
        }
      }
      if (product.id == 12) {
        this.c12 += 1;
        if (this.c12 <= 1) {
          this.pushdata(product);
        } else {
          var cat12 = this.findindex(product);
          this.carts[cat12].qty += 1;
          this.carts[cat12].total = this.carts[cat12].qty * this.carts[cat12].price;
        }
      }
      if (product.id == 13) {
        this.c13 += 1;
        if (this.c13 <= 1) {
          this.pushdata(product);
        } else {
          var cat13 = this.findindex(product);
          this.carts[cat13].qty += 1;
          this.carts[cat13].total = this.carts[cat13].qty * this.carts[cat13].price;
        }
      }
      if (product.id == 14) {
        this.c14 += 1;
        if (this.c14 <= 1) {
          this.pushdata(product);
        } else {
          var cat14 = this.findindex(product);
          this.carts[cat14].qty += 1;
          this.carts[cat14].total = this.carts[cat14].qty * this.carts[cat14].price;
        }
      }
      if (product.id == 15) {
        this.c15 += 1;
        if (this.c15 <= 1) {
          this.pushdata(product);
        } else {
          var cat15 = this.findindex(product);
          this.carts[cat15].qty += 1;
          this.carts[cat15].total = this.carts[cat15].qty * this.carts[cat15].price;
        }
      }
      if (product.id == 16) {
        this.c16 += 1;
        if (this.c16 <= 1) {
          this.pushdata(product);
        } else {
          var cat16 = this.findindex(product);
          this.carts[cat16].qty += 1;
          this.carts[cat16].total = this.carts[cat16].qty * this.carts[cat16].price;
        }
      }
      if (product.id == 17) {
        this.c17 += 1;
        if (this.c17 <= 1) {
          this.pushdata(product);
        } else {
          var cat17 = this.findindex(product);
          this.carts[cat17].qty += 1;
          this.carts[cat17].total = this.carts[cat17].qty * this.carts[cat17].price;
        }
      }
      if (product.id == 18) {
        this.c18 += 1;
        if (this.c18 <= 1) {
          this.pushdata(product);
        } else {
          var cat18 = this.findindex(product);
          this.carts[cat18].qty += 1;
          this.carts[cat18].total = this.carts[cat18].qty * this.carts[cat18].price;
        }
      }
      if (product.id == 19) {
        this.c19 += 1;
        if (this.c19 <= 1) {
          this.pushdata(product);
        } else {
          var cat19 = this.findindex(product);
          this.carts[cat19].qty += 1;
          this.carts[cat19].total = this.carts[cat19].qty * this.carts[cat19].price;
        }
      }
      if (product.id == 20) {
        this.c20 += 1;
        if (this.c20 <= 1) {
          this.pushdata(product);
        } else {
          var cat20 = this.findindex(product);
          this.carts[cat20].qty += 1;
          this.carts[cat20].total = this.carts[cat20].qty * this.carts[cat20].price;
        }
      } 
    },
    pushdata(product) {
      this.carts.push({
        id: product.id,
        name: product.title,
        price: product.price,
        image: product.image,
        qty: 1,
        total: product.price,
      });
    },
    findindex: function (product) {
      for (var i = 0; i < this.carts.length; i++) {
        if (this.carts[i].id == product.id) {
          return i;
        }
      }
      return -1;
    },
    minusqty: function (item) {
      item.qty -= 1;
      if (item.qty <= 1) {
        item.qty = 1;
      }
      item.total = item.price * item.qty;
    },
    plusqty: function (item) {
      item.qty += 1;
      item.total = item.price * item.qty;
    },
    removeproduct(item) {
      if (confirm("You want to Delete ??")) {
        var index = this.carts.indexOf(item);
        this.carts.splice(index, 1);
        if (item.id == 1) {
          this.c1 = 0;
        }
        if (item.id == 2) {
          this.c2 = 0;
        }
        if (item.id == 3) {
          this.c3 = 0;
        }
        if (item.id == 4) {
          this.c4 = 0;
        }
        if (item.id == 5) {
          this.c5 = 0;
        }
        if (item.id == 6) {
          this.c6 = 0;
        }
        if (item.id == 7) {
          this.c7 = 0;
        }
        if (item.id == 8) {
          this.c8 = 0;
        }
        if (item.id == 9) {
          this.c9 = 0;
        }
        if (item.id == 10) {
          this.c10 = 0;
        }
        if (item.id == 11) {
          this.c11 = 0;
        }
        if (item.id == 12) {
          this.c12 = 0;
        }
        if (item.id == 13) {
          this.c13 = 0;
        }
        if (item.id == 14) {
          this.c14 = 0;
        }
        if (item.id == 15) {
          this.c15 = 0;
        }
        if (item.id == 16) {
          this.c16 = 0;
        }
        if (item.id == 17) {
          this.c17 = 0;
        }
        if (item.id == 18) {
          this.c18 = 0;
        }
        if (item.id == 19) {
          this.c19 = 0;
        }
        if (item.id == 20) {
          this.c20 = 0;
        }
      }
    },
    total: function () {
      var sum = 0;
      this.carts.forEach(function (product) {
        sum += product.total;
      });
      return sum;
    },
  },
};
</script>

<style scoped>
.qty-minus {
  cursor: pointer;
  margin-right: 20px;
}
.qty-plus {
  cursor: pointer;
  margin-right: 20px;
}
</style>
