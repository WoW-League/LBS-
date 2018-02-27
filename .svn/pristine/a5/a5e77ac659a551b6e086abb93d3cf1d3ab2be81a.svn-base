var app1 = new Vue({
    el: "#app1",
    data: {
        //声明空数组，进行数据接收，最后传递到前端页面
        itemList: []
    },
    //向data数组里添加数据
    mounted: function() {
        this.getData();
    },
    methods: {
        getData: function() {
            var self = this;
            this.$http.get("http://192.168.0.104:8085/data/firstService.json").then(function(res) {
                var selData = res.body
                self.itemList = selData;
            })
        },
        jumpTwo: function(id,name){
            // var posText = document.querySelector('.indexPos').innerHTML;
            var thisSrc = 'publish-demand.html?id='+id+'&name='+name;
            window.location.href = thisSrc; 
        }
    }
});
var app2 = new Vue({
    el: "#app2",
    data: {
        itemList: [],//所有的数据
        checkedNames: [],//选中的三级故障
        current: -1,//二级映射三级
        classifyId: -1,//一级映射二级
        isActive: false,//一级分类导航激活
        webUrl: window.location.search,
        stairText: '',//解析地址得到的一级名字
        toggle: true
    },
    //向data数组里添加数据
    mounted: function() {
        this.getData();
    },
    methods: {
        getData: function() {
            this.$http.get("http://192.168.0.104:8085/data/getService.json").then((res) => {
                var selData = res.body;
                this.itemList = selData;
                this.$nextTick(function(){
                    //对应二级子菜单
                    var urlStr = this.webUrl,
                        urlArr = urlStr.split('='),
                        urlId = this.GetQueryString("id");
                    this.stairText = decodeURI(urlArr[2]);
                    this.classifyId = urlId;  
                    this.isActiveo = true;
                });
            })    
        },
        intoThree: function(index){
            this.current = index;
            this.toggle = false;
            this.isActive = true;
        },
        GetQueryString: function (name){
            var reg = new RegExp("(^|&)"+ name +"=([^&]*)(&|$)");
            var r = window.location.search.substr(1).match(reg);
            if(r!=null)return  unescape(r[2]); return null;
        },
        toTwo: function(){
            this.toggle = true;
            this.isActive = false;
        },
        toThree: function(){
            this.toggle = false;
            this.isActive = true;            
        },
        selectChecked: function(item){
            if(typeof item.checked == 'undefined'){
                this.$set(item,"checked",true)
            } else{
                item.checked = !item.checked;
            }
        }
    }
});
var app4 = new Vue({
    el: '#app4',
    data: {
        addressState: false,
        webUrl: window.location.search,
        indexPosText: ''
    },
    mounted: function() {
        this.getData();
    },
    methods: {
        getData: function(){
            this.$nextTick(function(){
                this.indexPosText = sessionStorage.getItem("curAddress");
                // var urlStr = this.webUrl,
                //     urlArr = urlStr.split('=');
                //this.indexPosText = decodeURI(urlArr[2].split('&')[0]);
            })
        },
        toAdress: function(){
            this.addressState = true;
            var that = this;
            window.addEventListener('message', function(event) {
                that.addressState = false;
                // 接收位置信息，用户选择确认位置点后选点组件会触发该事件，回传用户的位置信息
                var loc = event.data;
                if (loc && loc.module == 'locationPicker') {//防止其他应用也会向该页面post信息，需判断module是否为'locationPicker'
                    document.getElementById('mapPage').style.display = 'none';
                    that.indexPosText = loc.poiaddress
                    // document.write(JSON.stringify(loc, null, 4))
                  // console.log('location', JSON.stringify(loc, null, 4));  
                }                                
            }, false); 
        },
        confirmAddress: function(){
            this.indexPosText = document.querySelector('#detail_add').innerHTML;
            this.addressState = false;
        }
    }
})
