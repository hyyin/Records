# js download 文件方案

## 背景： 需要用token验证身份，window.open无法携带token（httpheader）

* jquery.form.js ajaxSubmit方法
* download.js
* filesaver.js
* 如下code

```
exportDocument(data, fileName) {
        let myHeaders = new Headers();
        myHeaders.append('Content-Type', 'application/json');
        return fetch(`${CommonUtil.getTargetUrlPrefix(SAComponents.COMPONENT_ASSESSMENTAUTHORING)}/api/template/templateExport`, {
            body: JSON.stringify(data),
            headers: myHeaders,
            method: 'POST'

        }).then(r => r.blob()).then(blob => {
            const reader = new FileReader();
            reader.onload = (e) => {
                let data = atob(e.target.result.split('base64,')[1]);
                data = data.substring(1, data.length - 1);
                data = "data:;base64," + data;
                let eleLink = document.createElement('a');
                eleLink.download = fileName + '.docx';
                eleLink.href = data;
                document.body.appendChild(eleLink);
                eleLink.click();
                document.body.removeChild(eleLink);
            }
            let red = reader.readAsDataURL(blob);
        });
    }

```
