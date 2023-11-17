<!--
 * @Description:
 * @Author: panrui
 * @Date: 2023-07-14 15:10:25
 * @LastEditTime: 2023-11-17 10:47:13
 * @LastEditors: prui
 * 不忘初心,不负梦想
-->

## 最后更新时间(2023-11-17)

- [官方文档](https://artskydj.github.io/jsPDF/docs/index.html)

```js
downPdf() {
    const that = this
    let secondDivContent = document.getElementById('pdf');
    secondDivContent.style.display = 'block'
    document.getElementById('pdf').scrollTop = 0;
    html2canvas(document.querySelector('#pdf'), {
        allowTaint: true,
        useCORS: true,
        scale: 2,
        height: $('#pdf')[0].clientHeight,
        width: $('#pdf')[0].clientWidth,
        ignoreElements: function(element) {
            if (element.classList.contains('dialog-footer')) {
                return true;
            }
            return false;
        }
    }).then(function (canvas) {
            let pageData = canvas.toDataURL('image/jpeg', 1.0);
            let PDF = new jspdf.jsPDF('', 'pt', 'a4');
            that.dialogVisible_report = false
            let contentWidth = canvas.width;
            let contentHeight = canvas.height;
            let position = 10;
            let imgWidth = 595.28 - 20;
            let leftHeight = contentHeight;
            let pageHeight = contentWidth / 592.28 * 841.89;
            let imgHeight = (592.28 / contentWidth * contentHeight);
            if (imgHeight > 840) {
                imgHeight = 800
            }
            PDF.addImage(pageData, 'JPEG', 10, position, imgWidth, imgHeight);
            PDF.save('子公司安全诊断报告.pdf');
        }
    )
}
```
