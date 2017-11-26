<template>
    <div id="app">
        <styleEditor ref="styleEditor" :code="currentStyle"></styleEditor>
        <resumeEditor ref="resumeEditor" :markdown="currentMarkdown" :enableHtml="enableHtml"></resumeEditor>
    </div>
</template>
<script>
import styleEditor from './components/styleEditor'
import resumeEditor from './components/resumeEditor'

export default {
    name: 'app',
    components: {
        styleEditor,
        resumeEditor
    },
    data() {
        return {
            intervalTime: 50,
            currentStyle: '',
            currentMarkdown: '',
            enableHtml: false,
            myStyle: [`/* Hello!  I'm lion1ou.
*
*  又到了一年招聘季
*
*  作为一个正想跳槽的前端er
*
*  要跳槽那肯定得有份简历吧！
*
*  不说那么多了，说写就写！
*
*/


/* 先给自己模拟一个sublime Text吧 */

.styleEditor {
    font-size:1.2em;
    width: 45vw;
    height: 95vh;
    border: 1px solid;
    background: rgb(39, 40, 34);
    color: rgb(248, 248, 242);
    padding: 1em;
    margin: .5em;
    overflow: auto;
    border-radius: .5em;
}

/* 作为程序员的编辑器，没有代码高亮怎么行？ */

.token.comment {
    color: rgb(104, 100, 83);
}

.token.selector {
    color: rgb(249, 38, 95);
}

.token.property {
    color: rgb(102, 217, 231);
}

.token.punctuation {
    color: rgb(249, 151, 32);
}

.token.function {
    color: rgb(166, 226, 44);
}


/* 还是不够炫酷，那就加点 3D 效果吧 */

html {
    -webkit-perspective: 1000px;
    perspective: 1000px;
}

.styleEditor {
    position: fixed;
    left: 0;
    top: 0;
    transform: rotateY(10deg) translateZ(-100px);
    -webkit-transform: rotateY(10deg) translateZ(-100px);
}


/* 接下来给自己准备一个MarkDown编辑器 */

.resumeEditor {
    position: fixed; right: 0; top: 0;
    width: 48vw; height: 95vh;
    padding: 1em;
    margin: .5em;
    border: 1px solid;
    background: white;
    border-radius: .5em;
}


/* 还是一样来点 3D 效果 */

.resumeEditor {
    font-size:1.2em;
    color: #222;
    overflow: auto;
    -webkit-transform: rotateY(-10deg) translateZ(-100px);
    transform: rotateY(-10deg) translateZ(-100px);
}


/* 好了，我开始写简历了 */

`,
                `
/* 这个简历好像差点什么
 * 对了，这是 Markdown 格式的，我需要变成对HR小姐姐更友好的格式
 * 简单，用开源工具翻译成 HTML 就行了
 */
`,
                `
/* 再对 HTML 加点样式 */

.resumeEditor h1 {
    display: block;
    text-align: center;
    margin: 1em 0 .5em .25em;
}

.resumeEditor h2 {
    display: inline-block;
    border-bottom: 1px solid;
    padding: .2em 0;
    margin: 1em 0 .5em .25em;
}

.resumeEditor h3 {
    display: block;
    margin: 1em 0 .25em 1em;
}

.resumeEditor ul {
    list-style: none;
}

.resumeEditor ul> li::before {
    content: '•';
    margin-right: .75em;
}

.resumeEditor a:visited {
    color: #000;
}

/*
 *   先写到这吧，
 *   需求查看详细简历
 *   请移步： http://lion1ou.win/resume/
 */
`
            ],
            myMarkdown: `# 罗德忠/lion1ou

## 个人信息

- 罗德忠/1992.7/本科
- 工作年限：3年
- 个人博客：[http://lion1ou.win](http://lion1ou.win)
- Github：[https://github.com/lion1ou](https://github.com/lion1ou)
- Email：lion1ou@163.com

## 项目经验

### 杭州乐刻网络技术有限公司（2017.3 - 至今）

* [乐刻运动教练端](https://h5.leoao.com/coach/#/coach/index/todo)
* [乐刻运动用户端](https://h5.leoao.com/mStation/?#/)
* [乐刻活动页项目](https://h5.leoao.com/multiple/punchCard/transcript.html?outerId=1496619)

### 上海建坤信息技术有限责任公司（2015.3 - 2017.3）

* 建坤大型智慧园区管理平台 -- 工作流管理系统模块
* ble蓝牙环境监测APP
* 气象博物馆自动导览APP

## 个人项目

* 简历模板： [静态页面简历模板](https://github.com/lion1ou/resume) 、[动态加载简历模板](https://github.com/lion1ou/resume2)
* 知识沉淀： [GitBook 项目](https://github.com/lion1ou/gitbook)、[个人博客](http://lion1ou.win)
* 工具库：[ltools](https://github.com/lion1ou/ltools)，[gulp脚手架](https://github.com/lion1ou/gulp_generator)

## 致谢
感谢您花时间阅读我的简历，期待能有机会和您共事。

`
        }
    },
    created() {
        this.codingResume();
    },
    methods: {

        codingResume: async function() {

            await this.codingShowStyle(0)
            await this.codingShowResume();
            await this.codingShowStyle(1);
            await this.showHtml();
            await this.codingShowStyle(2);
        },
        showHtml: function() {
            return new Promise((resolve, reject) => {
                this.enableHtml = true;
                console.log(this.myStyle, this.myMarkdown);
                resolve();
            })
        },
        codingShowStyle: function(n) {
            return new Promise((resolve, reject) => {
                let intervalTime = this.intervalTime;
                let showStyle = (async function() {
                    let style = this.myStyle[n]
                    if (!style) {
                        return
                    }
                    let beforeNLength = 0;
                    for (var i = 0; i < n + 1; i++) {

                        beforeNLength += this.myStyle[i].length
                        console.log(this.myStyle[i].length);
                    }
                    console.log('beforeNLength', beforeNLength);
                    let fromLength = beforeNLength - style.length;
                    console.log('fromLength', fromLength);
                    if (this.currentStyle.length < beforeNLength) {
                        let codingLength = this.currentStyle.length - fromLength;
                        console.log('codingLength', codingLength);

                        let char = style.substring(codingLength, codingLength + 1) || ' ';
                        console.log(char);
                        this.currentStyle += char;
                        if (style.substring(codingLength - 1, codingLength) == '\n' && this.$refs.styleEditor) {
                            this.$nextTick(() => {
                                this.$refs.styleEditor.goBottom();
                            })
                        }
                        setTimeout(showStyle, intervalTime)
                    } else {
                        resolve()
                    }

                }).bind(this)
                showStyle()
            })
        },
        codingShowResume: function() {
            return new Promise((resolve, reject) => {
                let intervalTime = this.intervalTime;
                let length = this.myMarkdown.length;
                let showResume = () => {
                    if (this.currentMarkdown.length < length) {

                        let char = this.myMarkdown.substring(this.currentMarkdown.length, this.currentMarkdown.length + 1) || ' ';
                        console.log(char);

                        this.currentMarkdown += char;
                        if (this.myMarkdown.substring(length - 1, length) === '\n' && this.$refs.resumeEditor) {
                            this.$nextTick(() => {
                                this.$refs.resumeEditor.goBottom()
                            })
                        }
                        setTimeout(showResume, intervalTime)
                    } else {
                        resolve()
                    }
                }
                showResume()
            })
        }
    }
}
</script>
<style>
#app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
}

html {
    min-height: 100vh;
}

* {
    transition: all .3s;
    -webkit-transition: all .3s;
}
</style>
