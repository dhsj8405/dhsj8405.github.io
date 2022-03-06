---

layout: post
title: '웹팩 로더설정(+바벨로더)'
subtitle: '웹팩 로더설정(+바벨)'
categories: devlog
tags: react
comments: true

---

# webpack-practice 복사해서 사용
`npm init -y`  

# 로더, 바벨로더 설정
 `npm i -D webpack webpack-cli webpack-dev-server babel-loader style-loader css-loader sass-loader node-sass @babel/core @babel/cli @babel/cli @babel/preset-env @babel/preset-react`    

- @babel/preset-env   
    Babel 플러그인을 모아둔 것  
    = 어떤 코드를 어떻게 변환할지에 대한 규칙을 모아둔 것  
 - css-loader   
css형식의 파일을 javascript형식의 데이터로 변환해주는 역할

- style-loader  
자바스크립트로 변경된 스타일시트를 동적으로 돔에 추가할 수 있게 해주는 역할

# react dom 사용
 `npm i react react-dom`

## 설치 확인 (package.json)
![image](https://user-images.githubusercontent.com/60701130/156878728-f70815f9-21a4-4672-bef6-45b2513622c0.png)

## webpack.config.js loader 설정
```
const path = require('path');

module.exports = {
    mode: 'development', 
    
    // 의존성 분석을 src밑에 index.js부터한다 == entry 속성은 최상위 자바스크립트를 의미
    // 이 속성에 명시된 파일을 기준으로 의존성 트리를 만들어 하나의 번틀 파일을 만든다.
    entry: path.resolve('./src/index'),     

    // output 속성: 컴파일 + 번들링 된 js 파일이 저장될 경로와 이름을 지정한다.
    output: {
        path: path.resolve('public'),
        filename: 'bundle.js',
        assetModuleFilename: 'assets/images/[hash][ext]'       //모듈에 이미지 걸리면 퍼블릭으로 옮기면서 이름 해싱해서보냄
    },
    
    // module 속성은 로더를 설정해주는 역할
    // webpack은 js뿐만 아니라 Loader를 이용하여 CSS나 이미지, 웹폰트, jSX, VUE 등 
    // 다양한 종류의 파일을 함께 번들링 할 수 있는데 그 설정을 여기서 하는 것이다.
    module:{
        rules: [{
            test: /\.js$/i,      
            exclude: /node_modules/, //정규표현식 //트랜스파일링(코드변환)하는데 node_modules라이브러리들은 빼라 
            use: ['babel-loader'] 
        },{
            test : /\.(sa|sc|c)ss$/i,                          //sass,scss,css로 끝나는 모든파일 : .을 쓰기위해 이스케이프(\) 써줌 i:ignorecase, sass가 scss편하게쓰게해주는것
            use : ['style-loader', 'css-loader','sass-loader'] //use 배열안에 여러 로더를 설정할 경우 로더의 실행 순서는 오른쪽에서 왼쪽순으로 실행
        },{
            test: /\.(png|gif|jpe?g|svg|ico|tiff?|bmp)$/i,         //$ :끝        e?g e가없어도됨 
            type: 'asset/resource'
        }]
    },
        devtool: "eval-source-map",                     //에러났을때 에러위치를 번들링.js로 표시해서 원래소스랑 매핑해주는것
    devServer: {
        // contentBase: path.resolve('public'),
        host: '0.0.0.0',
        port: 9999,
        // inline: true,
        hot: false,
        compress: true,
        historyApiFallback: true            // 가상~~ 404 났을때 메인으로도림
    }
}
```

## babel.config.json 설정
```
{
    "presets": [
        ["@babel/preset-env", {
            "targets": {
                "ie": "11",
                "edge": "89",
                "firefox": "92",
                "chrome": "90",
                "opera": "76",
                "safari" : "15"
            }

        }],
        "@babel/react" 
    ]
}
```
## package.json의 스크립트 추가하기
 ```
 "scripts": {
    "start": "npx webpack serve --progress",
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "npx webpack"
  },
```

## 어플리케이션 실행
`npx webpack`  
`npx webpack serve --progress`

## localhost:9999 접속 결과
![image](https://user-images.githubusercontent.com/60701130/156908159-ee4167b8-c7fe-4302-a6eb-b1b5751ccea1.png)
