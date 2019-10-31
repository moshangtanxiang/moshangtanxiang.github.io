---
title: iview对接
date: 2019-10-31 10:52:46
categories:
- iview
---

## 表格数据
	
```
	  <Table stripe :columns="columns1" :data="list"></Table>
	  <div class="block" style="text-align: center;margin: 20px auto;">
	      <Page :total="total" 		// 分页
	        :page-size="pageSize" 
	        @on-change="changepage" 
	        show-total  
	        show-elevator 
	        :current="pageNum" />
	  </div>
```

html部分由上，columns的title代表表头，key绑定接受后台传入字段名，数据部分绑定list，自动循环。
操作按钮需要手写，如其他字段一样；如数据无误，打印params会有相关行内数据，获取相关数据进行操作。

```
		data() {
			return{
				list: [],
				columns1: [
					{
                        title: '缺工岗位类别',
                        align:"center",
                        key: 'general',
                        children:
                            [
                              {
                                  title: '普工',
                                  key: 'lackWorker',
                                  align: 'center',

                              },
                              {
                                  title: '技术',
                                  key: 'lackTechnician',
                                  align: 'center',

                              },
                                {
                                  title: '管理人员',
                                  key: 'lackManager',
                                  align: 'center',
                                    width:110

                              },
                                {
                                  title: '其他',
                                  key: 'lackOther',
                                  align: 'center',

                              }
                            ]
                    },
                    {
				        title: '操作',
				        key: 'other2',
				        align: 'center',
				          render: (h, params) => {
				            return h("div", [
				              h(
				                "Button",
				                {
				                  props: {
				                    type: "primary",
				                    size: "small"
				                  },
				                  style: {
				                    marginRight: "5px",
				                    width:"24px",
				                    height:"24px",
				                    color:"#ffffff",
				                    backgroundColor:"#12BD42",
				                    backgroundRadius:"4px",
				                    borderRadius:"4px"
				                  },
				                  on: {
				                    click: () => {
				                      this.modal2 = true;
				                      let id = params.row.id
				                      api.qi_planEditor({id: id}).then((res) => {
				                        this.formValidate2= res.data;
				                      })
				                    }
				                  }
				                },
				              )
				            ]);
				          }
    				}
                ]
            }
        }
```

以下翻页，其他data、接口等方面同vue类似。
```
 //页码
    changepage(value) {
        let datas = {
            pageNum: value,
            pageSize: this.pageSize,
        }
        api.qi_plan(datas).then(res=>{
            this.list = res.data.list;
        })
    },
    ```
## 数据导出
接下来是一种导出的写法，隐藏表单提交导出所需文件：
```
 		<form  action="接口地址" target="_blank" id="formdata" method ="post"  style="display: none;">
          <input type="hidden" name="模糊查询字段名" :value="字段值" />
        </form>


      	<Button style="color:#0066ff" @click="reportEmploryExport()">
	        <Icon custom="i-icon iconevent_up" size="14"/>
	        导出
	    </Button>


    reportEmploryExport() {
        $('#formdata').submit();
    },
            ```


