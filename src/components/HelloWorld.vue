<template>
  <div class="hello">
    <Container>
      <circles/>
      <template v-for="(item, index) in userInfo">
        <div :key="index">
        <colum-flex-container >
        <CenterLine></CenterLine>
        <line-dot-container :left="index%2 === 1">
          <CircleLineContainer v-if="index%2 === 1">
            <DataContainer :left="true">
              <LogoContainer>
              <img width="25px" src="../assets/logo.png" alt=""/>
              </LogoContainer>
              <DateContainer>
              {{ dateFormat(item.registered)}}
              </DateContainer>
              {{item.name.first}}&nbsp;{{item.name.last}}
            </DataContainer>
            <circles/>
            <InfoContainer></InfoContainer>
          </CircleLineContainer>
          <div>
            <CircleWithDot></CircleWithDot>
          </div>
          <CircleLineContainer  v-if="index%2 === 0">
            <InfoContainer></InfoContainer>
            <circles/>
            <DataContainer>
              <logo-container>
                <img width="25px" src="../assets/logo.png" alt=""/>
              </logo-container>
              <DateContainer>
                {{dateFormat(item.registered)}}
              </DateContainer>
              <TextContainer>
                {{item.name.first}}&nbsp;{{item.name.last}}
              </TextContainer>
            </DataContainer>
          </CircleLineContainer>
        </line-dot-container>

        </colum-flex-container>
        <CenterLine></CenterLine>
        </div>
      </template>
      <circles/>
    </Container>
  </div>

</template>

<script>
import styled from 'vue-styled-components'
import data from '../json/Vue_timeline.json'
const Container = styled('div')`
text-align: -webkit-center;
`
const InfoContainerProps = {
  left: false
}
const DataContainer = styled('div' ,InfoContainerProps)`
    position: absolute;
    right: -135px;
    display: flex;
    flex-direction: column;
    width: 100px;
    left: ${props=>props.left ? '-135px' : ''};
    align-items:${props=>props.left ? 'center' : 'center'};
`
const CircleLineContainer = styled('div')`
    display: flex;
    flex-direction: row;
    align-items: center;
    position: relative;
`
const ColumFlexContainer = styled('div')`
    display: flex;
    flex-direction: column;
    align-items: center;
`

const LineDotContainer = styled('div',InfoContainerProps)`
    display: flex;
    width: 240px;
    justify-content: ${props=>props.left ? 'left' : 'right'};
`
const Circles = styled('div')`
 height:25px;
 width:25px
 border-radius: 50%;
 background-color:#0b5184
`
const CircleWithDot = styled('div')`
     height: 13px;
    width: 13px;
    border-radius: 50%;
    border: 8px solid #0b5184;
`

const InfoContainer = styled('div') `
background-color:#0b5184
 height:8px;
 width:80px
`
const CenterLine = styled('div')`
height: 40px;
width: 8px;
background-color: #0b5184
`
const LogoContainer = styled('div')`
    margin-left: auto;
    margin-right: auto;
`
const DateContainer = styled('span')`
   font-weight: bold;
   color: #0b5184;
`
const TextContainer = styled('span')`
   color: #585858
`
// #585858
export default {
  name: 'HelloWorld',
  data() {
    return {
      userInfo: []
    }
  },
  props: {
    msg: String
  },
  components:{
    Container,
    Circles,
    LogoContainer,
    DateContainer,
    TextContainer,
    InfoContainer,
    ColumFlexContainer,
    CircleLineContainer,
    CenterLine,
    CircleWithDot,
    LineDotContainer,
    DataContainer
  },
  methods: {
    dateFormat(date) {
      return date.split(',')[1]
    }
  },
  mounted() {
    data.sort((a,b) =>  new Date(a.registered.split(',')[1]) - new Date(b.registered.split(',')[1]));
    this.userInfo = data
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
