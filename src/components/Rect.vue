<template>
    <div ref="resizeRef" id="container">
        <svg ref="svgRef"></svg>
    </div>
   <audio id="song">
  <source src="Song.mp3" type="audio/mp3">
Your browser does not support the audio element.
</audio> 
</template>
 
<script>
import { onMounted, ref } from 'vue';
import { select, easeLinear } from 'd3';

import useResizeObserver from '@/use/resizeObserver';
var fail = 0
const drawRect = (height, index, svg) => {
    const w = 200;
    let rect = svg
        .append('rect') //添加一个矩形
        .attr('x', index * w)
        .attr('y', -1 * height)
        .attr('width', w)
        .attr('height', height)
        .attr('fill', 'green');
    return rect;
    // var rectTran = rect.transition()
    //                     .delay(delay)
    //                     .duration(2000)
    //                     .ease(easeLinear)
    //                     .attr("y",500);
    // rectTran.remove();

    // console.log(rect,props,resizeState,rectTran)
};
const tranRect = (rect, delay) => {
    var rectTran = rect
        .transition()
        .delay(delay)
        .duration((500+parseInt(rect._groups[0][0].attributes['height'].value))*5)
        .ease(easeLinear)
        .attr('y', 600)
        .on("end", ()=>{
            if(rect._groups[0][0].attributes['fill'].value!='transparent' && fail == 0){
                fail = 1
                console.log(rect)
                alert('fail')
                rectTran.remove();
            }
        });
    // rectTran.remove();
    
    return rectTran;
};

export default {
    name: 'RectAm',
    props: ['data'],
    setup(props) {
        const svgRef = ref(null);
        const { resizeRef, resizeState } = useResizeObserver();
        var datestart = new Date();
        

        onMounted(() => {
            const data = [
                [100, 3000],
                [200, 4000],
                [100, 3500],
                [300, 5000],
                [100, 5750],

            ];
            const svg = select(svgRef.value);
            let rects = [];
            let transs = [];
            const checkLine = 450
            const bgbtnHeight = 600
            const delta = 25
            let preP= -1;
            for (let i = 0; i < data.length; i++) {
                let rand = Math.floor(Math.random() * 4);
                while (rand == preP){
                    rand = Math.floor(Math.random() * 4);
                }
                preP = rand
                rects.push({
                    rect: drawRect(data[i][0], rand, svg),
                    delay: data[i][1],
                    pos: rand,
                });
            }
            svg.append('rect') //添加一个矩形
                .attr('x', 0)
                .attr('y', bgbtnHeight)
                .attr('width', 800)
                .attr('height', 2000)
                .attr('fill', '#ccc');
            svg.append('rect') //添加一个矩形
                .attr('x', 0)
                .attr('y', -200)
                .attr('width', 800)
                .attr('height', 200)
                .attr('fill', '#ccc');

            let btn1 = svg
                .append('rect') //添加一个矩形
                .attr('x', 0)
                .attr('y', 0)
                .attr('width', 200)
                .attr('height', bgbtnHeight)
                .attr('fill', '#D3D3D3')
                .lower();
            let btn2 = svg
                .append('rect') //添加一个矩形
                .attr('x', 200)
                .attr('y', 0)
                .attr('width', 200)
                .attr('height', bgbtnHeight)
                .attr('fill', '#D3D3D3')
                .lower();
            let btn3 = svg
                .append('rect') //添加一个矩形
                .attr('x', 400)
                .attr('y', 0)
                .attr('width', 200)
                .attr('height', bgbtnHeight)
                .attr('fill', '#D3D3D3')
                .lower();
            let btn4 = svg
                .append('rect') //添加一个矩形
                .attr('x', 600)
                .attr('y', 0)
                .attr('width', 200)
                .attr('height', bgbtnHeight)
                .attr('fill', '#D3D3D3')
                .lower();
            let start = svg
                .append('rect') //添加一个矩形
                .attr('x', 300)
                .attr('y', 300)
                .attr('width', 200)
                .attr('height', 100)
                .attr('fill', '#ff9900');

            let starttxt= svg
                .append('text')
                .text("start")
                .attr('x', 300)
                .attr('y', 300)
                .attr("font-size", 50)
                .attr('dx', 50)
                .attr('dy', 65)
                .attr('fill', '#ffffff');
            
            let startcolorhover = '#ff9900';
            let startcolorout = '#ff6600';
            let flag = 1;
            var starttime = 0;
            select('body')
                .on('keydown', (event) => {
                    fail = 1
                    const keyCodeChar = String.fromCharCode(event.keyCode);
                
                    const checkRectDown = (x) => {
                        const filter = rects.filter(
                            (item) =>
                                parseInt(
                                    item.rect._groups[0][0].attributes['x']
                                        .value
                                ) === x
                        );
                        for (const item of filter){
                            if(item.rect._groups[0][0].attributes['fill'].value == 'transparent'){
                                continue; 
                            } 
                            const y = parseFloat(item.rect._groups[0][0].attributes['y'].value);
                            // abs(y+h-350) < 1
                            if(Math.abs(y+ parseInt(item.rect._groups[0][0].attributes['height'].value)-checkLine) <= delta){
                                item.rect._groups[0][0].attributes['fill'].value = 'transparent'
                                fail = 0
                            }
                            break
                        }
                        if(fail ==1){
                            alert("fail")
                        }

                    };
                    const keyDownMap = {
                        A() {
                            btn1.attr('fill', '#DCDCDC');
                            checkRectDown(0);
                        },
                        S() {
                            btn2.attr('fill', '#DCDCDC');
                            checkRectDown(200);
                        },
                        D() {
                            btn3.attr('fill', '#DCDCDC');
                            checkRectDown(400);
                        },
                        F() {
                            btn4.attr('fill', '#DCDCDC');
                            checkRectDown(600);
                        },
                    };
                    keyDownMap[keyCodeChar]?.();
                })
                .on('keyup', () => {
                    btn1.attr('fill', '#D3D3D3');
                    btn2.attr('fill', '#D3D3D3');
                    btn3.attr('fill', '#D3D3D3');
                    btn4.attr('fill', '#D3D3D3');
                });

            start
                .on('click', (event) => {
                    var audio = new Audio('Song.mp3');
                    svg.append('rect') //添加一个矩形
                    .attr('x', 0)
                    .attr('y', checkLine)
                    .attr('width', 800)
                    .attr('height', 2)
                    .attr('fill', '#FF4500');
                    audio.play();
                    start.attr('fill', 'transparent').lower();
                    starttxt.attr('fill', 'transparent').lower();
                    startcolorhover = 'transparent';
                    startcolorout = 'transparent';
                    starttime =
                        datestart.getTime() + datestart.getMilliseconds();
                    if (flag == 1) {
                        console.log(rects);
                        rects.forEach((rect) => {
                            transs.push(tranRect(rect['rect'], rect['delay']));
                        });

                        flag = 0;
                    }
                    console.log(event, starttime);
                })
                .on('mouseover', (event) => {
                    start.attr('fill', startcolorhover);
                    console.log(event);
                })
                .on('mouseout', (event) => {
                    start.attr('fill', startcolorout);
                    console.log(event);
                });
            console.log(
                props,
                resizeState,
                btn1,
                btn2,
                btn3,
                btn4,
                data,
                start
            );
        });

        return { svgRef, resizeRef };
    },
};
</script>
<style>
#container {
    height: 500px;
    z-index: 1;
}
</style>
