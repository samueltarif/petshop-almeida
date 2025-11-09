<template>
  <div class="shower-3d" aria-hidden="true">
    <div class="scene">
      <div class="pipe"></div>
      <div class="elbow"></div>
      <div class="head"></div>
      <div class="spray">
        <div class="jet j1"></div>
        <div class="jet j2"></div>
        <div class="jet j3"></div>
        <div class="jet j4"></div>
        <div class="jet j5"></div>
      </div>
      <div class="drops">
        <div class="drop d1"></div>
        <div class="drop d2"></div>
        <div class="drop d3"></div>
      </div>
    </div>
  </div>
</template>

<script setup>
// Ícone de chuveiro 3D com cabeça, cano e jatos de água
</script>

<style scoped>
.shower-3d {
  width: 64px;
  height: 64px;
  perspective: 800px;
  display: inline-block;
}

.scene {
  position: relative;
  width: 100%;
  height: 100%;
  transform-style: preserve-3d;
  transform: rotateX(16deg) rotateY(-18deg);
}

.pipe {
  position: absolute;
  left: 10px;
  bottom: 40px;
  width: 6px;
  height: 20px;
  border-radius: 4px;
  background: linear-gradient(180deg, #aeb8c1 0%, #7a8894 100%);
  box-shadow: 0 6px 10px rgba(0,0,0,.12), inset 0 2px 2px rgba(255,255,255,.6);
  transform: translateZ(12px);
}

.elbow {
  position: absolute;
  left: 12px;
  bottom: 48px;
  width: 18px;
  height: 6px;
  border-radius: 4px;
  background: linear-gradient(180deg, #aeb8c1 0%, #7a8894 100%);
  box-shadow: 0 6px 10px rgba(0,0,0,.12), inset 0 2px 2px rgba(255,255,255,.6);
  transform: translateZ(14px);
}

.head {
  position: absolute;
  left: 26px;
  bottom: 44px;
  width: 18px;
  height: 10px;
  border-radius: 8px 8px 10px 10px;
  background: radial-gradient(80% 60% at 50% 40%, #dde4ea 0%, #b8c2cb 60%, #8d99a6 100%);
  box-shadow: 0 8px 12px rgba(0,0,0,.14), inset 0 3px 4px rgba(255,255,255,.5);
  transform: translateZ(16px) rotateZ(-8deg);
}

.spray { position: absolute; left: 30px; bottom: 34px; transform: translateZ(16px); }
.jet {
  position: absolute;
  width: 2px;
  height: 16px;
  border-radius: 2px;
  background: linear-gradient(180deg, rgba(120,200,230,.95) 0%, rgba(90,180,220,.7) 60%, rgba(70,160,200,.5) 100%);
  box-shadow: 0 2px 6px rgba(0,0,0,.12);
}
.jet.j1 { left: 0px;  transform: rotateZ(-6deg); }
.jet.j2 { left: 4px;  transform: rotateZ(-2deg); }
.jet.j3 { left: 8px;  transform: rotateZ(0deg); }
.jet.j4 { left: 12px; transform: rotateZ(2deg); }
.jet.j5 { left: 16px; transform: rotateZ(6deg); }

.drops { position: absolute; left: 32px; bottom: 18px; transform: translateZ(14px); }
.drop {
  position: absolute;
  width: 4px;
  height: 6px;
  border-radius: 50% 50% 60% 60%;
  background: radial-gradient(60% 60% at 50% 40%, rgba(140,210,240,.9) 0%, rgba(90,180,220,.75) 60%, rgba(70,160,200,.55) 100%);
  box-shadow: 0 2px 4px rgba(0,0,0,.12);
}
.drop.d1 { left: 0px;  animation: drip 1400ms ease-in infinite; }
.drop.d2 { left: 8px;  animation: drip 1600ms ease-in infinite; }
.drop.d3 { left: 16px; animation: drip 1500ms ease-in infinite; }

@keyframes drip {
  0% { transform: translateY(0) translateZ(0); opacity: 0; }
  20% { opacity: 1; }
  100% { transform: translateY(12px) translateZ(-2px); opacity: 0; }
}

.shower-3d:hover .scene {
  transform: rotateX(13deg) rotateY(-14deg) translateZ(2px);
  transition: transform 180ms var(--ease-standard);
}
</style>