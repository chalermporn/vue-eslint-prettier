<template>
  <div>
    <DslTitleBack
      title="detail"
      :mode="mode"
      @click="goToBack()"
      screen="NNN:MMM2"
    />
    <DslCollapse
      v-model="isOpen1"
      title="ข้อมูลลูกหนี้และผู้เกี่ยวข้อง"
      :is-collapse="true"
    >
      <template v-slot:body>
        <Form
          v-if="mode === 'edit'"
          ref="formValidate"
          :model="formValidate"
          :rules="ruleValidate"
          label-position="top"
        >
          <Row
            gutter="30"
            type="flex"
            justify="space-between"
            class="code-row-bg"
          >
            <Col span="5" :xs="24" :sm="12" :md="12" :lg="6">
              <FormItem label="Name" prop="name">
                <DslInput
                  v-model="formValidate.name"
                  placeholder="Enter your name2222"
                ></DslInput>
              </FormItem>
              <FormItem label="Name" prop="name">
                <Input
                  v-model="formValidate.name2"
                  placeholder="Enter your name"
                ></Input>
              </FormItem>
            </Col>
            <Col span="5" :xs="24" :sm="12" :md="12" :lg="6">
              <FormItem label="E-mail" prop="mail">
                <Input
                  v-model="formValidate.mail"
                  placeholder="Enter your e-mail"
                ></Input>
              </FormItem>
            </Col>
            <Col span="5" :xs="24" :sm="12" :md="12" :lg="6">
              <FormItem label="City" prop="city">
                <Select
                  v-model="formValidate.city"
                  placeholder="Select your city"
                >
                  <Option value="beijing">New York</Option>
                  <Option value="shanghai">London</Option>
                  <Option value="shenzhen">Sydney</Option>
                </Select>
              </FormItem>
            </Col>
            <Col span="5" :xs="24" :sm="12" :md="12" :lg="6">
              <FormItem label="Date">
                <DatePicker
                  type="date"
                  placeholder="Select date"
                  v-model="formValidate.date"
                ></DatePicker>
              </FormItem>
            </Col>

            <Col span="5" :xs="24" :sm="12" :md="12" :lg="6">
              <FormItem label="Gender" prop="gender">
                <RadioGroup v-model="formValidate.gender">
                  <Radio label="male">Male</Radio>
                  <Radio label="female">Female</Radio>
                </RadioGroup>
              </FormItem>
            </Col>
          </Row>
        </Form>
      </template>
      <template v-slot:footer>
        <DslButtonClear @click="handleReset('formValidate')" />
        <DslButtonSubmit @click="handleSubmit('formValidate')" />
      </template>
    </DslCollapse>
  </div>
</template>

<script>
// import i18n from "@/i18n";
export default {
  name: "InvoiceDetail",
  components: {},
  data() {
    return {
      isOpen1: "open",
      formTop: {},
      formItem: {},
      isCollapsed: false,
      theme1: "light",
      menuActive: [1],
      value: 1,
      topmenu: [
        {
          id: 1,
          icon: "ios-home",
          label: "หน้าแรก"
        },
        {
          id: 2,
          icon: "ios-keypad",
          label: "จัดการข้อมูล"
        },
        {
          id: 3,
          icon: "ios-keypad",
          label: "แจ้งหนี้"
        },
        {
          id: 4,
          icon: "ios-keypad",
          label: "ติดตามหนี้"
        },
        {
          id: 5,
          icon: "ios-keypad",
          label: "ปรับโครงสร้างนี้"
        },
        {
          id: 6,
          icon: "ios-keypad",
          label: "กำหนดการเงืีอนไข"
        }
      ],
      columns7: [
        {
          type: "selection",
          width: 60,
          align: "center"
        },
        {
          title: "#",
          key: "no",
          width: 50
        },
        {
          title: "CIF",
          key: "cif",
          width: 140
        },
        {
          title: "เลขที่บัตรประจำตัวประชาชน",
          key: "personalId",
          width: 180
        },
        {
          title: "Name",
          key: "name",
          render: (h, params) => {
            return h("div", [
              h("Icon", {
                props: {
                  type: "person"
                }
              }),
              h("strong", params.row.name)
            ]);
          }
        },
        {
          title: "Age",
          key: "age"
        },
        {
          title: "Address",
          key: "address"
        },
        {
          title: "Action",
          key: "action",
          width: 150,
          align: "center",
          render: (h, params) => {
            return h("div", [
              h("Button", {
                props: {
                  icon: "ios-eye",
                  type: "text"
                },
                style: {
                  marginRight: "5px",
                  fontSize: "20px"
                },
                on: {
                  click: () => {
                    this.show(params.index);
                  }
                }
              })
              // h('Button', {
              //   props: {
              //     type: 'error',
              //     size: 'small'
              //   },
              //   on: {
              //     click: () => {
              //       this.remove(params.index)
              //     }
              //   }
              // }, 'Delete')
            ]);
          }
        }
      ],
      data6: [
        {
          no: 1,
          cif: "000000664345",
          personalId: "1729900093587",
          name: "John Brown",
          age: 18,
          address: "New York No. 1 Lake Park"
        },
        {
          no: 2,
          name: "Jim Green",
          age: 24,
          address: "London No. 1 Lake Park"
        },
        {
          no: 3,
          name: "Joe Black",
          age: 30,
          address: "Sydney No. 1 Lake Park"
        },
        {
          no: 4,
          name: "Jon Snow",
          age: 26,
          address: "Ottawa No. 2 Lake Park"
        }
      ],
      formValidate: {
        name: "",
        mail: "",
        city: "",
        gender: "",
        interest: [],
        date: "",
        time: "",
        desc: ""
      },
      ruleValidate: {
        name: [
          {
            required: true,
            message: "The name cannot be empty",
            trigger: "blur"
          }
        ],
        mail: [
          {
            required: true,
            message: "Mailbox cannot be empty",
            trigger: "blur"
          },
          { type: "email", message: "Incorrect email format", trigger: "blur" }
        ],
        city: [
          {
            required: true,
            message: "Please select the city",
            trigger: "change"
          }
        ],
        gender: [
          { required: true, message: "Please select gender", trigger: "change" }
        ],
        interest: [
          {
            required: true,
            type: "array",
            min: 1,
            message: "Choose at least one hobby",
            trigger: "change"
          },
          {
            type: "array",
            max: 2,
            message: "Choose two hobbies at best",
            trigger: "change"
          }
        ],
        date: [
          {
            required: true,
            type: "date",
            message: "Please select the date",
            trigger: "change"
          }
        ],
        time: [
          {
            required: true,
            type: "string",
            message: "Please select time",
            trigger: "change"
          }
        ],
        desc: [
          {
            required: true,
            message:
              this.$t("coreMsg.validator.notEmpty") +
              this.$t("txt.description"),
            trigger: "blur"
          },
          {
            type: "string",
            min: 20,
            message: this.$t("coreMsg.validator.noEnough"),
            trigger: "blur"
          }
        ]
      }
    };
  },
  computed: {
    id() {
      return this.$route.params.id;
    },
    mode() {
      return this.$route.params.mode;
    }
  },
  methods: {
    handleSubmit(name) {
      this.$refs[name].validate(valid => {
        if (valid) {
          this.$Message.success("Success!");
        } else {
          //
        }
      });
    },
    handleReset(name) {
      this.$refs[name].resetFields();
    },
    goToBack() {
      //
      this.$router.push("/invoice/search-data2");
    },
    menuChange() {
      //
    },
    toggleCollapse() {
      this.$refs.side.toggleCollapse();
    },
    change() {
      this.isCollapsed = !this.isCollapsed;
    },
    changed() {
      // console.log(res)
    },
    show(index) {
      this.$Modal.info({
        title: "User Info",
        content: `Name：${this.data6[index].name}<br>Age：${this.data6[index].age}<br>Address：${this.data6[index].address}`
      });
    },
    remove(index) {
      this.data6.splice(index, 1);
    }
  },
  watch: {
    isCollapsed() {
      // console.log(val)
    }
  }
};
</script>
<style lang="less" scoped>
.layout-logo {
  width: 140px;
  height: 30px;
  background: #5b6270;
  border-radius: 3px;
  float: left;
  position: relative;
  top: 15px;
  left: 20px;
}
.layout-demo-con {
  height: 100%;
}
</style>
