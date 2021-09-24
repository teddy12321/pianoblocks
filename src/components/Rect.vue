<template>
    <div ref="resizeRef" id="container">
        <svg ref="svgRef"></svg>
    </div>
   <audio id="song">
  <source src="Pi Slowed.mp3" type="audio/mp3">
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
        .attr('fill', 'black');
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
                alert('Game Over')
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
        var accurate = 250

        onMounted(() => {
            const data = [
                [100, 6150+accurate],
                [100, 6450+accurate],
                [100, 6750+accurate],
                [100, 7050+accurate],
                [100, 7350+accurate],
                [100, 7650+accurate],
                [100, 7950+accurate],
                [50, 8550+accurate],
                [100, 8700+accurate],
                [100, 9000+accurate],
                [100, 9300+accurate],
                [100, 9600+accurate],
                [100, 9900+accurate],
                [100, 10200+accurate],
                [100, 10500+accurate],
                [100, 10800+accurate],
                [100, 11100+accurate],
                [100, 11700+accurate],
                [100, 12300+accurate],
                [200, 12600+accurate],
                [100, 13200+accurate],
                [200, 13800+accurate],
                [200, 14400+accurate],
                [200, 15000+accurate],
                [200, 15600+accurate],
                [100, 16500+accurate],
                [100, 17100+accurate],
                [100, 17400+accurate],
                [100, 17700+accurate],
                [100, 18000+accurate],
                [100, 18300+accurate],
                [100, 18600+accurate],
                [100, 18900+accurate],
                [100, 19200+accurate],
                [100, 20100+accurate],
                [100, 20400+accurate],
                [100, 21000+accurate],
                [100, 21300+accurate],
                [100, 21900+accurate],
                [100, 22200+accurate],
                [100, 22500+accurate],
                [100, 22800+accurate],
                [100, 23100+accurate],
                [100, 23400+accurate],
                [100, 23700+accurate],
                [100, 24000+accurate],
                [100, 24300+accurate],
                [100, 24600+accurate],
                [100, 24900+accurate],
                [100, 25550+accurate],
                [100, 25700+accurate],
                [100, 26300+accurate],
                [100, 26600+accurate],
                [100, 26900+accurate],
                [50,  27200+accurate],
                [50,  27350+accurate],
                [50,  27500+accurate],
                [50,  27750+accurate],
                [50,  27900+accurate],
                [50,  28050+accurate],
                [100,  28950+accurate],
                [100,  29550+accurate],
                [100,  29850+accurate],
                [100,  30150+accurate],
                [100,  30450+accurate],
                [100,  30750+accurate],
                [100,  31050+accurate],
                [100,  31350+accurate],
                [100,  31650+accurate],
                [100,  31950+accurate],
                [100,  32250+accurate],
                [100,  32550+accurate],
                [100,  32850+accurate],
                [100,  33350+accurate+1*300],
                [100,  33350+accurate+2*330],
                [100,  33350+accurate+3*330],
                [100,  33350+accurate+4*330],
                [100,  33350+accurate+5*330],
                [100,  33350+accurate+6*330],
                [100,  33350+accurate+7*330],
                [100,  33350+accurate+8*330],
                [100,  33350+accurate+9*330],
                [100,  33350+accurate+10*330],
                [100,  33350+accurate+11*330],
                [100,  33350+accurate+12*330],
                [100,  33350+accurate+13*330],
                [100,  33350+accurate+14*330],
                [100,  33350+accurate+15*330],
                [100,  33350+accurate+16*330],
                [100,  33350+accurate+17*330],
                [100,  33350+accurate+18*330],
                [100,  33350+accurate+19*330],
                [100,  33350+accurate+20*330],
                [100,  33350+accurate+21*330],
                [100,  33350+accurate+22*330],
                [100,  33350+accurate+23*330],
                [100,  33350+accurate+24*330],
                [100,  33350+accurate+25*330],
                [100,  33350+accurate+26*330],
                [100,  33350+accurate+27*330],
                [100,  33350+accurate+28*330],
                [100,  33350+accurate+29*330],
                [100,  33350+accurate+30*330],
                [100,  33350+accurate+31*330],
                [100,  33350+accurate+32*330],
                [100,  33350+accurate+33*330],
                [100,  33350+accurate+34*330],
                [100,  33350+accurate+35*330],
                [100,  33350+accurate+36*330],
                [100,  33350+accurate+37*330],
                [100,  33350+accurate+38*330],
                [100,  33350+accurate+39*330],
                [100,  33350+accurate+40*330],
                [100,  33350+accurate+41*330],
                [100,  33350+accurate+42*330],
                [100,  33350+accurate+43*330],
                [100,  33350+accurate+44*330],
                [100,  33350+accurate+45*330],
                [100,  33350+accurate+46*330],
                [100,  33350+accurate+47*330],
                [100,  33350+accurate+48*330],
                [100,  33350+accurate+49*330],
                [100,  33350+accurate+50*330],
                [100,  33350+accurate+51*330],
                [100,  33350+accurate+52*330],
                [100,  33350+accurate+53*330],
                [100,  33350+accurate+54*330],
                [100,  33350+accurate+55*330],
                [100,  33350+accurate+56*330],
                [100,  33350+accurate+57*330],
                [100,  33350+accurate+58*330],
                [100,  33350+accurate+59*330],
                [100,  33350+accurate+60*330],
                [100,  33350+accurate+61*330],
                [100,  33350+accurate+62*330],
                [100,  33350+accurate+63*330],
                [100,  33350+accurate+64*330],
                [50,  33350+accurate+65.5*330],
                [100,  33350+accurate+66*330],
                [100,  33350+accurate+67*330],
                [100,  33350+accurate+68*330],
                [100,  33350+accurate+69.5*330],
                [100,  33350+accurate+70*330],
                [100,  33350+accurate+71.5*330],
                [150,  33350+accurate+72*330],
                [100,  33350+accurate+75*330],
                [100,  33350+accurate+76*330],
                [100,  33350+accurate+78*330],
                [100,  33350+accurate+81*330],
                [100,  33350+accurate+82*330],
                [100,  33350+accurate+84*330],
                [100,  33350+accurate+85*330],
                [100,  33350+accurate+86*330],
                [100,  33350+accurate+90*330],
                [100,  33350+accurate+92*330],
                [100,  33350+accurate+94*330],

            ]
            const svg = select(svgRef.value);
            let rects = [];
            let transs = [];
            const checkLine = 450
            const bgbtnHeight = 600
            const delta = 100
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
                .text("Start")
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
                            alert("Game Over")
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
                    var audio = new Audio('Pi Slowed.mp3');
                    svg.append('rect') //添加一个矩形
                    .attr('x', 0)
                    .attr('y', checkLine)
                    .attr('width', 800)
                    .attr('height', 10)
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
