import React from 'react';

import { makeStyles } from '\@material-ui/core/styles';

import Button from '\@material-ui/core/Button';

const useStyles = makeStyles({

root: {

background: 'linear-gradient(45deg, \#FE6B8B 30%, \#FF8E53 90%)',

border: 0,

borderRadius: 3,

boxShadow: '0 3px 5px 2px rgba(255, 105, 135, .3)',

color: 'white',

height: 48,

padding: '0 30px',

},

});

export default function Hook() {

const classes = useStyles();

return \<Button className={classes.root}\>Hook\</Button\>;

}

As you can see in this example, we're using the makeStyles function to generate
a hook called useStyles which create a CSS classes *object* which contains the
keys of the styles object we created. In this example, it doesn't actually
matter that we call this class root, because we reference it like a variable
when we add it to the Button's className prop. As you will read in the advanced
customization guide:

Every component provides a className property which is always applied to the
root element.

That's so important! That means we can always safely overwrite the root
element's CSS. In this above example, we are changing the Button's background
color, height, text color. Did you know that the Button is just a simple
HTML \<button\> tag with a \<span\> for the text? There's a simplicity to
underlying HTML that you should get to know.

This is pretty much it, taken from a contained Button example:

\<button class="MuiButtonBase-root MuiButton-root MuiButton-contained
MuiButton-containedPrimary" tabindex="0" type="button"\>

\<span class="MuiButton-label"\>Primary\</span\>

\<span class="MuiTouchRipple-root"\>\</span\>

\</button\>

How to style inner HTML elements in Material UI

Okay so you might be wondering, how to I know how to target these inner HTML
elements of Material UI? Where is this documented? Welcome to CSS rules! Let's
quote from the "Overriding styles with classes" section. Read the following very
closely!

When the className property isn't enough, and you need to access deeper
elements, you can take advantage of the classes object property to customize all
the CSS injected by Material-UI for a given component. The list of classes for
each component is documented in the component API page, you should refer to the
CSS section and rule name column. For instance, you can have a look at the
Button CSS API. Alternatively, you can use the browser dev tools.

To summarize, you can find the names of the CSS rules in the second half of the
component's API page. For the Button, you can see that there is a root rule, and
a label rule. If you're too lazy to go to the API page and just want to inspect
the HTML, you can see above that there is a -label rule right on
the \<span\> element. Target that rule by using the classes prop with an object
containing those keys from your classes you got from useStyles.

That looks like this:

\<Button

classes={{

root: classes.root, // class name, e.g. \`classes-nesting-root-x\`

label: classes.label, // class name, e.g. \`classes-nesting-label-x\`

}}

\>

classes nesting

\</Button\>

\</head\>

\<**!-- 0-pseudo classes:**- are the built in classes like
a:hover/visited{color:blue} here hover and visited are pseudo classes,

**1-** aur hm kisi elemnt ki class ko b pseudo class k saath use kr skty hn like
elemnt.htmlclassname:pseudoclass{color:white**}**

**,2**-kisi element pe agr hover kre tu koi dosra elemnt b show krva skty hn
like this div:hover h1{display:block}mtlb jo elemnts ko show krvana hu unko
container k ander rakhty hn jesy ye ab h1 ko show krvay ga jo k div k ander h,

**3**-first psceudo child classes like this p:first-child{color:blue}ye classes
basically jo conatiners k ander first elemnt huga us pe style kr dy ga,aur agr
bht sary let suppose bold words hu bold tag k ander paragraph me tu phr usko
aesy select kre gy like this -- p b:first-child{color:blue} aur agr bht sary
paragraph hu un me se first bold chaay hu tu phr  aesy likhy gy --p:first-child
b{color:blue}

 **4-** agr hm kisi particular numbering like even,odd,ya sequence pe style krna
hu tu phr p:nth-child{} esko class ko use kre gy**,**

**5- last-child aur first-child same hn aur nth-child **

**1-pseudo elements:**-**ye basically kisi ek elemnt k content pe kaam krta h
jbk pseudo classes pory elemnt pr kaam krty hn** ,pseudo elemnts ko aesy use kr
skty hn like this p::first-letter/line{font-size:40px},aur agr kisi ek letter pe
kaam krna hu kisi line k tu phr hm html me class ka use kr k css kr skty hn like
this **p.classname::first-letter**{color:red},aur letter k saath saath kisi hm
line ko b ek saath css kr skty hn like this **p::first-ltter
::first-line{color:red},**aur hm esi trh **p/.classname::before/after/marker aur
b bht se hn use kr skty hn{content:"kch b yaha kr skty hn like img insert kr
stkyhn,url aur text wgra"}** 

    **A-there are three ways for styling 1-inline**:- mean on single
element/tag,

    **2-internal:- basically jitny b elements ya tag hu gy same wo sb ko style
hu jaay ga mostly on a single page we apply this,**

**    if we apply external css then the priority of external will be applied not
internal but if inline is already used then its priority will be prefer**

**    but if we want to prefer any one of these three then we will use
!important in that prefer style either inline,external,internal**

   ** 3-external** :-mtlb jo parent pe style kre gy

**    B- selectors:-**

      ** (a)-1-element,2-id,3-class,4-grouping(mtlb k 2,3, jitny b krna chay
unko aktha style kr skty hn like id,class,element{color:white}**)

         **  -2 attribute selectors:**- mtbl jb hmko kisi attribute pe style
krna hu tu phr ye selector use krty hn jesa k classes,dosry parameters like this
[class \|='.desing']{color:red} mtlb k ye property hr us pe apply hugi jiski
class ka name desing ya followed by hyphen hu,aur [class\^='.design'] jaha b
design class aay usko apply kr do,aur agr koi aesi selct krna chaty hn jaha end
with design hu like this [class \$='design'],aur agr sari classes pe apply krna
chaty hn jo design se start hu tu phr [class\*='design'],aur hm ne agr kisi
container m kahien class use ki hue h tu phr aesay huga p[class]{color;red}
,same for href,target aur dosri properties kliy use kr skty hn like this
a[href]{colore:red} aur agr parameters ko values pass ki hue hn tu phr unko
values se access kr skty hn like this a[target='value']{color:red}

          ** -3 \>combinator**:- ye basically hm kisi container class ko agr
child pe direct use krna chaay tu ye \> operator use krty hn

   ** C- difference between postion and align is that in postion we set the
location of the a elemnt and in alignment we set the content **

    **D-link States**:- unvisited,visited,hover,active(when a button clik that
time its color of state)

**v.vIMp E-Display(inline,block mean if display none then visibilty property
will also do the same ) in css inline srf wohe jaga lety hn jitna unka size huta
h aur bki dono pori line ka size lety hn es liy enko block elements kehty hn,**

**    so if we want to change them into one another we use display properties
aur inline always ek he line me aa  jaaty hn unko alg krny kliy break tag ka use
kr skty hn**

**    also when we use display then we cant use the margin top  and bottom for
block  but other margin type can use  also for all the margin if we use the
inline-block**

**    similar for inline we cant change the height and width mtlb k dono me jo
properties hm use ni kr skty wo hm inline-block k through kr skty hn**

**vvImp F-Position:**-**static(ye postion by default aati h so esko mention krny
ki zaroorat ni h),relative(ye apni original/static postion se apni postion set
krta h aur es me b top,left,right wgra set krny huty hn es me parent ko relative
rakhna huta h aur child ko phr koi b position dy skty agr aesa ni krty tu child
es k parent mtlb es se pechly waly element ka ya page ki postion k hisaab se set
kr le ga),fixed(es me ye huta h k jo elemnt huta h wo apni postion pe fixed
rehta h mtlb jb screen scroll krty hn tu bki scroll hu jaaty hn but ye ni huta h
),sticky(es me ye huta h k jo elemnt huta h uski jo b position pixel k according
set ki huti either on left,right,top ya bottom jb b wo us pixel position pe
pohnchta h tu phr ja kr wo stick hu jata h aur bki sb scroll huta h),absolute(es
me element apny parent k hisaab se position leta h aur css me hmy top,left,right
wgra b position k saath mention krny huty hn aur es me agr koi gap aata h tu wo
uska jo next elemnt huta h fill kr dta h mtlb k wo gap ki jaga pe aa jata h)**

**(z-index:- ye basically do box k content ko kitna overlap kr stka h aur ye us
waqt use huta jb hm ne position set ki huti h aur eski value plus aur minus me
dety hn)**

**vvImp G-CSS FLEX:**- the flex layout allows responsive elements within a
container to be automatically arranged depending upon screen size mtlb k
different devices ki screens me ,ye b display property ko follow krty hn like
this
.class{display:flex;flex-wrap:wrap,frex-direction:row/column/reverse,align-items:flexe-center/start/end,justify-content:flex-end/start/center}--these
were the properties for the flex box aur agr flex items ki properties krni hu tu
phr \<p style="order:7";flex-basis(ye basically height/width pe work krta
h):50px;flex-grow(ye jesy jesy screen ka size  bdhta h ye size ko adjust krta
h):3;flex-shrink(ye screen k accord. ye jis item pe apply huga usk  size ko tezi
se shrink krega:3)\>5\</p\> tu ab ye es paragraph ko 7index pe display krega hm
en propeties ki values ko aktha b likh skty hn like this \<style
=flex:20,30,10px\>

**H-Float and Clear**:-jesy hm inline aur block use krty thy wesy he ye use huty
hn float tb use huty hn jb inline elements ko ek he line me rakhna hu jb space
availble hu ye b basically layouts ko desing krny me use huty hn,agr hm ne kch
elements ki value float set kr rakhi hu aur ek aur elemnt le us me float set na
kre tu phr wo overlap kr jata h tu es problem ko overcome krny kliy clear ka use
krty hn phr like this .design{float:left},.deisgn1{clear:both},aur ji containers
ko ek he line me rakhna hu chaay left se ya right se mtlb jaha pe space hu tu
phr un containers ki tarteeb ko us hisaab se rakhy gy html me

**css topics **

**1-grid**

      es me rows aur columns huty hn aur jo items huti hn wo b elg se container
huty hn aur enki different properties huti hn like grid-column/row-start/end:1 3
ye columns/row ko merge kr k utna size le ly ga,shortcut way is
grid-column/row:1/3 ek aur b way h
grid-area:1gridcolumnstart/2gridrowstart/3gridcolumnend/4gridrowend

display:grid,grid-column/row-template:auto auto auto,ye basically height kliy
huta h aur row wala width kliy ,gap:10,20px agr srf ek value hu tu dono kliy
apply huga

justify-content: space -around--ye equal left/right se space leta h sb items
kliy externally ,space-between--ye items k dermiyaan equal space kr deta h,
similar start/end/center --mtlb k ye items ko start/end/center me kr deta h

grid kliy spert properties hn jesy k opr hn aur items kliy tag ya class k
through css apply kre gy

**2-Animations**

    div{position:relative,--ye agr ni dy gy tu movement ni hugi

animation-name:design,

animation -delay:2sec,

animation -iteration-count:3,

animation -ditection:reverse,

animation -timing-function:easein/out/linear

animation-duration:2sec

shortcut way to write all these properties

animation:design 2s linear 5s infinite reverse}

\@keyframe design {from{backgrndcolor:blue}

to{bckgrndcolor:red} esko likhny ka dosra way aesy b h
0%{left:10,top:20px;bgcolor:blue}50%{left:20,too:30px;bgcolor:red}70%{bgcolor:green}100%{bgcolor:
orange}}

**3-Transition to show the 2D/3D effect**

div{color:red,

border:5px,

bgcolor:10px

transition:width/height 5s

}

div:hover{width/height:100px,

transform:rotate/skew/scale/translate--ye basically 3D effect deti h ye property

transform:translate (x,y axis pe kitna rotate krna h,

transform:rotate(40deg),

transform:skew(45deg)--ye thoda thircha hu jata h es me

transform:scale(2,2)--ye basically width aur height mtlb size ko kam aur bdhata
h mtlb width ya height ko double krna h ya half hm ye kisi ek x ya y axis ki trf
b kr skty hn

ek aur shortcut treqa b h

transform: matrix ( es me opr wali sari properties apply kr skty hn like this
2,0.5,0.0,0.2)}--en transition properties ko hm animation me b from and to me b
pass kr skty h 

**4-Media Query**

it is applied for different devices like screen, print, speech and all

\@media screen/print  --  hm (orientation: portrait/landscape  property b use
krty hn, ye basically ek dosry k kam aur zda huny pe css apply krty hn like agr
height kam hu aur width zda hu tu phr jo b css apply krna chaaty hn wo apply kr
dy gy), (min/max-width:500px)-- ya dono function ko alg alg b use kr skty hn aur
and likh kr dono function ko b use kr skty hn ek saath aur agr koi ek cndtn
chlani hut tu phr do function k bw comma daal dy

{ 

div{

bgcolor:red

}

}

**Css selectors:**

1-element,ID,class

**Css selectors combination**

**1-**element k saath uski class -\>h1.class{},2-both class and
ID-\>\#Id.class{},3-ancesstors-\>parent .child{},tag.class child.class{},
.1stclass, .2ndclass{},\*{} for entire web page

**CSS Loading ways**

1-Inline-\>style on  tag,   2-Style element-\>head tag me ja kr waha style tag
me style krna 

3-External Style-\> in separate file css code rakha jaay

**Specificity 0,0,0,0**:here frst 0 is the inline element--\>where 0,1,0,0 this
showing the spcfcty of id,nd 0,0,1,0 this showing the class spcfcty

ID\>class\>tag ye show kr rahy hn k id ki sb se zda specificity h aur phr class
ki aur phr tag ki

Aur do classes hu ek he tag ki u m se dosri wli ki zda huti h,but agr agr
classes ,id se b zda kisi element ko pscfc banana hu tu phr classes se pehly us
tag ko b likh dy gy i.e. h1 class1 .class2{clor:red},aur agr me ne bht se
elements ko ek class pass kr rahi h tu phr us class ki spcfcty zda hugi**,esko
smjhny kliy ye bt yaad rakhy k id,class aur element ka ek ek number h so jiska
jitna zda number bnega uski utni zda spcfcty hugi thats set** i.e. h1 class1
class2 class3 {} aur h1class1class2{} es me pehly waly ki spcfcty zda hugi q kus
k numbers zda bn rahy hn,esi trh kisi block element ki spcfcty zd hugi inline
elemnet se aur agr body ki bt ki jaay tu uski sb se zda hugi q k s me sary
element aa jaaty hn,agr kisi ko strictly spcfc bnana hu tu us k saath
**important** likh diya jata h

**Colors Selecting Ways(RGB-\>\#000000 and these values start form 0to255):**

1-Simple select the color 2-By Decimal Number 0-9,3-Hexa Decimal-\>0toA-F where
A=10,F=15\#ffffffff,4-\>colors:rgb(255,0,0,0to1–and this value is transparency 0
mean no and 1 mean full transparency and btween them like 0.5 or something else
is best value),5-colors:hsl/hsla(0to360,saturation-\>0to100% this mean how much
color should be,0to100%lightness color 0%mean no lightness and 100%lightness,0)

**Measurements units:**

**1-pixel-\>**when the content size si fixed on the parent/page/screen then is
used

**2-Percentage-\>**it take the space by percentage of the entire
parent/page/screen size

**3-em-\>**it is mostly used for font when padding around the fonts and offers
the  actual fonts size of the parent font mtlb k agr koi parent font hu as a
element aur us kneechy koi box hu tu us box ko us font se padding deny kliy use
krty hn and the font size=16px =1em and we can use **2em=**32px and so on
1em=100%

**4-rem-\>**it is similar to em but it offers the size of the root of the
document/screen/page,mtlb k ye padding ko screen ya page keh le us k hisaab se
deta h aur opr wala us k opr koi font hu tu wo us k hisab se deta h and also em
is relative to the parent and rem is not

**5-vw/vh(view width/height)-\>1vw=1**% of the entire screen size either it is
width or height and not relative to the parent size

**Box Model/Container: **

Yr basically cpbm pattern ko follow krta h jis me(content,padding,border
radius,margin)

**FlexBox→yr layout ko design krny kliy use huta h aur ye one dimensional huta h
either row ya column at a time**

**1-Cross-axis;when layout will be row/main-axis then main will be column**

**2-Main-axis:when layout will be column/cross-axis mtlb row then main axis will
be horizontal** mtlb simple sa ye h k items ko main axis ya orw k hisaab se set
krna chaty hn ya cross-axis/column k i.e.
main-axis\<—-item1--item2---item3----------\> or cross-axis vertical k hisab se
item aay gi

Asl es me ye ek container huta h jis me flexibility(expandig/shrinkign of the
flex container) behave krta h jb hm container ko **display:flex** krty hn aur es
me aur containers ko b rakha jata h,aur es me jo content huta h usko hm set kr
skty hn **justify-content** ye property asl me jo containers flex container k
under huty hn unko row wise set krta h aur ek property huti h items ko jo en
containers k undr jo k content ko set krti h ,aur ek **align item** property
huti h jo k containers ko cross axis jo k column wise set krta h,aur ek **align
content** propert huti h jo k containers k both cross aur main axis k hisaab se
set krti h,**flex-wrap:wrap** b use krty hn mtlb row ko column aur column ko ro
wme change kr dta h,f**lex-shrink** jo hr continaers ko shrink huny se bcha leti
h aur f**lex-grow** jo k cotainers ko grow krti h mtlb k remaining space ko
occupy krti h aur agr chty hn k container double space occupy kre dosry
container k hisaab se tu phr **flex-basis:0** set kr dy aur
**align-self:center/end** mtlb k containers ko axis ya main axis k hisaab se set
krta h,**order;1/2/3** mtlb k kis item ko pehly ya bd me rkhna h,

Imp ye k ye properties alg alg content pe apply ki ja skti hn aur parent flex
box pe laga kr bkio ko wesy normal properties se set kr k b kiya ja skta h aur
**flex:0 1px** mtlb k ek sngle lign me b grow aur shrink property ko apply kr
skty hn

**CSS Grid:**

Container ko grid bnany kliy hm **display:grid** property use krty
hn,**grid-template-column/rows/auto:10px 20px/fr(same to flex
grow)/repeat(4,100px)/minmax(10px,20px/auto)** ye columns bna dy ga,gap deny
kliy rows k between **grd-row/column-gap/grid-gap:10px**,**grid-template-area:
‘header header’ ‘content suede1’ ‘contentsied2’  container1{grid-area:header}
contaienr2{grid-area:contet}** similar for all
,**container1{grid-column/row-start/end/grid-column/row:span 2  1/ -2 
1/2/3}**mtlb kknsa element pehly rakhna h aur knsa bd me,kesy algin krna h
containers**(justify-content/items:center),align-content/items:stretch**-\>mtlb
k cross axis aur main axis k saath item align krna ko aur un me content ko grid
container k undr ,difference ye h justify chaay content hu ya item wo apny
parent k hisaab se huta h set aur align apny parent k hisab se jis k undr wo lie
kr raha huta h, aur **justify/align-self:center**

**Difference between box-sizing and box-shadow**

**box-sizing** and **box-shadow** are both CSS properties used in styling
elements on a webpage, but they serve different purposes.

1.  **box-sizing**:

    -   **box-sizing** is a CSS property that determines how the total width and
        height of an element are calculated.

    -   It has two possible values: **content-box** and **border-box**.

    -   **content-box** is the default value. It calculates the width and height
        of an element excluding padding, border, and margin.

    -   **border-box** calculates the width and height of an element including
        padding and border, but not margin. This is often used to make layout
        calculations more predictable.

2.  **box-shadow**:

    -   **box-shadow** is a CSS property that adds a shadow effect to an
        element's frame.

    -   It allows you to specify the horizontal and vertical offsets of the
        shadow, the blur radius, the spread radius, and the color of the shadow.

    -   It's commonly used for creating depth and highlighting elements on a
        webpage.

In summary, **box-sizing** is used to control how the total dimensions of an
element are calculated, while **box-shadow** is used to add shadow effects to
elements. They serve different purposes in CSS styling.

**Grid and Flex:**

**For Parent Element (Grid Container):**

1.  **display: grid;**:

    -   This property is used to define a grid container.

    -   It establishes a new grid formatting context for its contents.

2.  **grid-template-columns** and **grid-template-rows**:

    -   These properties define the number and size of the columns and rows in
        the grid.

    -   They accept values such as absolute lengths, percentages, or **fr**
        units for flexible sizing.

3.  **grid-template-areas**:

    -   This property defines named grid areas.

    -   It allows you to visually lay out the grid by assigning names to
        specific areas, which can then be referenced in child elements.

4.  **grid-gap** or **gap**:

    -   This property defines the size of the gap between grid columns and rows.

    -   It is a shorthand for **grid-column-gap** and **grid-row-gap**
        properties.

5.  **justify-items** and **align-items**:

    -   These properties align grid items along the grid's columns and rows,
        respectively.

    -   They accept values like **start**, **end**, **center**, and **stretch**.

6.  **justify-content** and **align-content**:

    -   These properties align the grid within the container along the inline
        (row) and block (column) axes, respectively.

    -   They affect the spacing and alignment of the entire grid within its
        container.

**For Child Elements (Grid Items):**

1.  **grid-column** and **grid-row**:

    -   These properties specify the grid lines on which the item will be
        placed.

    -   They accept values like line numbers, line names, or **span** to specify
        the extent of the item across multiple tracks.

2.  **grid-area**:

    -   This property assigns the grid item to a named grid area specified in
        the parent grid container.

    -   It simplifies placement by referencing the named areas defined in the
        parent's **grid-template-areas**.

3.  **justify-self** and **align-self**:

    -   These properties override the alignment set by the grid container for
        individual grid items.

    -   They align items along the inline (row) and block (column) axes,
        respectively.

4.  **order**:

    -   This property specifies the order in which the grid items are displayed.

    -   It allows items to be visually re-ordered without changing the
        underlying HTML structure.

**For Parent Element (Flex Container):**

1.  **display: flex;**:

    -   This property is used to define a flex container.

    -   It establishes a flex formatting context for its contents.

2.  **flex-direction**:

    -   This property specifies the direction in which flex items are placed in
        the flex container.

    -   It can be set to **row**, **row-reverse**, **column**, or
        **column-reverse**.

3.  **flex-wrap**:

    -   This property determines whether flex items are forced onto a single
        line or can wrap onto multiple lines.

    -   Values include **nowrap**, **wrap**, and **wrap-reverse**.

4.  **justify-content**:

    -   This property aligns flex items along the main axis of the flex
        container.

    -   It controls the distribution of space between and around items.

    -   Values include **flex-start**, **flex-end**, **center**,
        **space-between**, and **space-around**.

5.  **align-items**:

    -   This property aligns flex items along the cross axis of the flex
        container.

    -   It defines how flex items are aligned within the flex container's line.

    -   Values include **flex-start**, **flex-end**, **center**, **baseline**,
        and **stretch**.

6.  **align-content**:

    -   This property aligns flex lines within the flex container when there is
        extra space on the cross-axis.

    -   It works similar to **justify-content**, but on the cross-axis.

    -   Values include **flex-start**, **flex-end**, **center**,
        **space-between**, **space-around**, and **stretch**.

**For Child Elements (Flex Items):**

1.  **flex-grow**:

    -   This property specifies how much a flex item can grow relative to the
        rest of the flex items in the flex container.

    -   It determines the distribution of free space when all flex items are
        flexible.

2.  **flex-shrink**:

    -   This property specifies how much a flex item can shrink relative to the
        rest of the flex items in the flex container.

    -   It determines how flex items shrink when there is not enough space in
        the flex container.

3.  **flex-basis**:

    -   This property sets the initial main size of a flex item.

    -   It specifies the initial size of the flex item before any remaining
        space is distributed.

4.  **flex**:

    -   This is a shorthand property for **flex-grow**, **flex-shrink**, and
        **flex-basis**.

    -   It allows you to specify all three values at once.

5.  **align-self**:

    -   This property allows the default alignment set by the flex container to
        be overridden for individual flex items.

    -   It aligns a flex item along the cross-axis, overriding the
        **align-items** value of the flex container.

**the differences between display, position, and float in CSS along with their
properties:**

1.  **Display:**

    -   The **display** property determines how an element behaves in the
        document flow.

    -   It controls the type of box generated by an element.

    -   Common values include:

        -   **block**: The element generates a block-level box, which means it
            takes up the entire width available and starts on a new line.

        -   **inline**: The element generates an inline-level box, which means
            it takes up only as much width as necessary and does not start on a
            new line.

        -   **inline-block**: The element generates a block-level box that flows
            like an inline element.

        -   **flex**: The element becomes a flex container and its children
            become flex items.

        -   **grid**: The element becomes a grid container and its children
            become grid items.

        -   **none**: The element is removed from the document flow and does not
            take up any space.

2.  **Position:**

    -   The **position** property specifies the positioning method used for an
        element.

    -   It works in conjunction with positioning properties like **top**,
        **bottom**, **left**, and **right**.

    -   Common values include:

        -   **static**: The default value where the element is positioned
            according to the normal flow of the document.

        -   **relative**: The element is positioned relative to its normal
            position in the document flow, but it can be moved using offset
            properties.

        -   **absolute**: The element is positioned relative to its nearest
            positioned ancestor, if any, or to the initial containing block
            otherwise.

        -   **fixed**: The element is positioned relative to the viewport and
            remains fixed even when the page is scrolled.

        -   **sticky**: The element is positioned based on the user's scroll
            position. It acts like **relative** positioning until it reaches a
            specified threshold, then it becomes **fixed**.

3.  **Float:**

    -   The **float** property specifies whether an element should float to the
        left or right within its containing element.

    -   It is often used for layouts where elements need to be floated next to
        each other.

    -   Common values include:

        -   **left**: The element floats to the left.

        -   **right**: The element floats to the right.

        -   **none**: The default value where the element does not float.

    -   Floating elements are taken out of the normal document flow, which can
        sometimes lead to layout issues.

In summary, **display** controls the type of box an element generates,
**position** determines how an element is positioned within its containing
element or the viewport, and **float** controls whether an element should float
to the left or right within its containing element. These properties are
fundamental for creating layouts and positioning elements on a webpage.

## Important Things to remember!About Box Model
1-if we are using box model with width like 100% and also set the padding,margin etc and this mean padding and margin will also include in this width,as width is calculated as by adding the padding either left,right,top,bottom,similar for margin and content,so if we set all these things then we have to minimize the width.
so what if we also want to add the margin,pading without changing the width then we have to set the **box-sizing:border-box** which automatically consider the margin,padding as the part of width so as by setting this now we will dont have scrolling on either left or right side.**line-height** property is basically set to height of text inside the box or `to center the text vertically`. to set the text in `center` we will do it as `horizontaly` by **text-align:center** , 
2-to set the two box consectively each other we will set the parent div clearfix and child float property,actually we do cear:both property in parent as we remove height from parent but we want that these two child's should have 
