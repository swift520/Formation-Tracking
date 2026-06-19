<script setup>
import { nextTick, onMounted, ref, watch } from 'vue'
import {
  Aim,
  Cpu,
  DataAnalysis,
  Position,
  RefreshRight,
} from '@element-plus/icons-vue'

const baseUrl = import.meta.env.BASE_URL || '/'
const letterSpeed = ref(1)
const realWorldSpeed = ref(1)
const trackingSpeed = ref(1)

const paperTitle = 'Graph-Based Multi-Agent Reinforcement Learning for Scalable UAV Formation Control and Target Tracking'

const navItems = [
  {
    label: 'Overview',
    shortLabel: 'Top',
    href: '#overview',
    icon: Cpu,
  },
  {
    label: 'Letter Formation',
    shortLabel: 'ICRA',
    href: '#letter-demo',
    icon: DataAnalysis,
  },
  {
    label: 'Formation Transition',
    shortLabel: 'Switch',
    href: '#transition-demo',
    icon: Aim,
  },
  {
    label: 'Target Tracking',
    shortLabel: 'Track',
    href: '#tracking-demo',
    icon: Position,
  },
]

const speedMarks = {
  0.5: '0.5x',
  1: '1x',
  1.5: '1.5x',
  2: '2x',
}

const letterDemos = [
  {
    id: 'letter12',
    image: 'icra1_1.png',
    video: 'video/1_final.mp4',
    label: 'Letter formation with 12 UAVs',
    meta: 'N = 12',
  },
  {
    id: 'letter18',
    image: 'icra1_2.png',
    video: 'video/2_final.mp4',
    label: 'Letter formation with 18 UAVs',
    meta: 'N = 18',
  },
]

const transitionDemos = [
  {
    id: 'transition-square',
    image: 'line.png',
    video: 'video/traj.mp4',
    label: 'Square to triangle',
    meta: 'Formation switch',
  },
  {
    id: 'transition-line',
    image: 'triangle.png',
    video: 'video/line.mp4',
    label: 'Vertical line to horizontal line',
    meta: 'Formation switch',
  },
]

function assetPath(path) {
  return `${baseUrl.replace(/\/?$/, '/')}${path.replace(/^\/+/, '')}`
}

function setVideoSpeed(group, speed) {
  document.querySelectorAll(`video[data-group='${group}']`).forEach((video) => {
    video.playbackRate = speed
  })
}

function playVideoGroup(group, speed) {
  document.querySelectorAll(`video[data-group='${group}']`).forEach((video) => {
    video.muted = true
    video.playbackRate = speed

    const playPromise = video.play()
    if (playPromise && typeof playPromise.catch === 'function') {
      playPromise.catch(() => {})
    }
  })
}

function restartVideos(group, speed) {
  document.querySelectorAll(`video[data-group='${group}']`).forEach((video) => {
    video.currentTime = 0
    video.playbackRate = speed

    const playPromise = video.play()
    if (playPromise && typeof playPromise.catch === 'function') {
      playPromise.catch(() => {})
    }
  })
}

function formatSpeed(value) {
  return `${Number(value).toFixed(1)}x`
}

watch(letterSpeed, (value) => {
  nextTick(() => setVideoSpeed('letter', value))
})

watch(realWorldSpeed, (value) => {
  nextTick(() => setVideoSpeed('real-world', value))
})

watch(trackingSpeed, (value) => {
  nextTick(() => setVideoSpeed('tracking', value))
})

onMounted(() => {
  nextTick(() => {
    playVideoGroup('letter', letterSpeed.value)
    playVideoGroup('real-world', realWorldSpeed.value)
    playVideoGroup('tracking', trackingSpeed.value)
  })
})
</script>

<template>
  <main class="project-page">
    <aside class="side-rail" aria-label="Section navigation">
      <a
        v-for="item in navItems"
        :key="item.href"
        :href="item.href"
        :aria-label="item.label"
      >
        <el-icon><component :is="item.icon" /></el-icon>
        <span>{{ item.shortLabel }}</span>
      </a>
    </aside>

    <section id="overview" class="hero-section">
      <div class="hero-grid" aria-hidden="true"></div>

      <div class="content-shell content-shell--hero">
        <div class="hero-copy">
          <h1 class="project-title">{{ paperTitle }}</h1>
        </div>

        <figure class="hero-showcase">
          <img :src="assetPath('framework_gnn_2.png')" alt="Graph-based MARL framework overview" class="hero-image">
        </figure>

        <div class="overview-grid">
          <p class="abstract-copy">
            This paper presents a graph-based multi-agent reinforcement learning framework for scalable UAV formation control and target tracking. The framework introduces a conflict-aware graph representation that aggregates neighborhood information through attention-based message passing, enabling each UAV to analyze both local interactions and global formation geometry. To generate agile and stable maneuvers, a hierarchical policy is designed that first selects motion primitives from a structured library and then refines them with continuous trajectory adjustments, ensuring smooth and dynamically feasible flight in cluttered environments. Extensive simulations and real-world experiments validate the proposed approach, demonstrating accurate target tracking, stable formation maintenance, and robust adaptation across varying swarm sizes and obstacle densities. In particular, policies trained on smaller swarms generalize effectively to larger ones without retraining, highlighting the scalability and practicality.
          </p>
        </div>
      </div>
    </section>

    <section id="letter-demo" class="paper-section paper-section--tint">
      <div class="content-shell content-shell--wide">
        <div class="section-heading">
          <h2>Letter Formation Demo</h2>
        </div>

        <p class="section-copy">
          This simulation setting places the swarm in a planar obstacle field and asks the agents to track a moving target while arranging into the letters "ICRA". Two swarm sizes are shown: 12 UAVs and 18 UAVs. In the trajectory plots, the red point marks the target, the dashed curve records its path, gray cylinders represent obstacles, and the colored UAV trajectories encode temporal progress from initialization to the final formation.
        </p>

        <div class="media-grid media-grid--two">
          <figure v-for="demo in letterDemos" :key="demo.id" class="media-card media-card--letter">
            <div class="media-meta">
              <span>{{ demo.meta }}</span>
              <strong>{{ demo.label }}</strong>
            </div>
            <img :src="assetPath(demo.image)" :alt="demo.label" class="media-image">
            <div class="media-frame media-frame--letter">
              <video
                :data-key="demo.id"
                data-group="letter"
                autoplay
                loop
                muted
                preload="auto"
                playsinline
                class="media-video media-video--contain"
                controlslist="nodownload nofullscreen noremoteplayback noaudio noplaybackrate"
              >
                <source :src="assetPath(demo.video)" type="video/mp4">
              </video>
            </div>
          </figure>
        </div>

        <div class="control-panel control-panel--speed">
          <span class="speed-label">Playback Speed: {{ formatSpeed(letterSpeed) }}</span>
          <div class="speed-slider">
            <el-slider v-model="letterSpeed" :min="0.5" :max="2" :step="0.1" :marks="speedMarks" :format-tooltip="formatSpeed" />
          </div>
          <el-button
            type="primary"
            :icon="RefreshRight"
            class="custom-button"
            @click="restartVideos('letter', letterSpeed)"
          >
            Restart Videos
          </el-button>
        </div>
      </div>
    </section>

    <section id="transition-demo" class="paper-section paper-section--light">
      <div class="content-shell content-shell--wide">
        <div class="section-heading">
          <h2>Formation Transition</h2>
        </div>

        <p class="section-copy">
          The real-world transition setting uses four Crazyflie 2.0 drones in an indoor space with static obstacles and a moving target car. Drone and target poses are provided by an HTC Vive tracking system, while a Livox LiDAR map supplies the obstacle layout for visualization. The two trials test whether the team can keep following the target while switching from square to triangle and from vertical line to horizontal line.
        </p>

        <div class="media-grid media-grid--two">
          <figure v-for="demo in transitionDemos" :key="demo.id" class="media-card">
            <div class="media-meta">
              <span>{{ demo.meta }}</span>
              <strong>{{ demo.label }}</strong>
            </div>
            <img :src="assetPath(demo.image)" :alt="demo.label" class="media-image">
            <div class="media-frame media-frame--wide">
              <video
                :data-key="demo.id"
                data-group="real-world"
                autoplay
                loop
                muted
                preload="auto"
                playsinline
                class="media-video"
                controlslist="nodownload nofullscreen noremoteplayback noaudio noplaybackrate"
              >
                <source :src="assetPath(demo.video)" type="video/mp4">
              </video>
            </div>
          </figure>
        </div>

        <div class="control-panel control-panel--speed">
          <span class="speed-label">Playback Speed: {{ formatSpeed(realWorldSpeed) }}</span>
          <div class="speed-slider">
            <el-slider v-model="realWorldSpeed" :min="0.5" :max="2" :step="0.1" :marks="speedMarks" :format-tooltip="formatSpeed" />
          </div>
          <el-button
            type="primary"
            :icon="RefreshRight"
            class="custom-button"
            @click="restartVideos('real-world', realWorldSpeed)"
          >
            Restart Videos
          </el-button>
        </div>
      </div>
    </section>

    <section id="tracking-demo" class="paper-section paper-section--tint">
      <div class="content-shell">
        <div class="section-heading">
          <h2>Target Tracking</h2>
        </div>

        <p class="section-copy">
          The tracking setting focuses on a moving ground target and a UAV team assigned to maintain a trapezoid formation. The scene includes obstacles that force local path adjustments while the group continues to keep target visibility and inter-agent spacing. The video emphasizes whether the formation stays coherent as the target moves through constrained regions.
        </p>

        <figure class="media-card media-card--tracking">
          <div class="media-meta">
            <span>Tracking task</span>
            <strong>Trapezoid formation around a moving target</strong>
          </div>
          <div class="media-frame media-frame--wide">
            <video
              data-key="tracking"
              data-group="tracking"
              autoplay
              loop
              muted
              preload="auto"
              playsinline
              class="media-video"
              controlslist="nodownload nofullscreen noremoteplayback noaudio noplaybackrate"
            >
              <source :src="assetPath('video/trac.mp4')" type="video/mp4">
            </video>
          </div>
        </figure>

        <div class="control-panel control-panel--speed">
          <span class="speed-label">Playback Speed: {{ formatSpeed(trackingSpeed) }}</span>
          <div class="speed-slider">
            <el-slider v-model="trackingSpeed" :min="0.5" :max="2" :step="0.1" :marks="speedMarks" :format-tooltip="formatSpeed" />
          </div>
          <el-button
            type="primary"
            :icon="RefreshRight"
            class="custom-button"
            @click="restartVideos('tracking', trackingSpeed)"
          >
            Restart Video
          </el-button>
        </div>
      </div>
    </section>
  </main>
</template>

<style scoped>
.project-page {
  --page-ink: #142033;
  --muted-ink: #5d6878;
  --paper: #f7faf9;
  --paper-warm: #fbfaf5;
  --panel: #ffffff;
  --panel-soft: rgba(255, 255, 255, 0.78);
  --line: rgba(20, 32, 51, 0.12);
  --line-strong: rgba(20, 32, 51, 0.2);
  --cyan: #0b8392;
  --cyan-soft: #e8f7f8;
  --green: #27795a;
  --amber: #b87819;
  --rose: #bf4d66;

  min-height: 100vh;
  color: var(--page-ink);
  background:
    linear-gradient(90deg, rgba(20, 32, 51, 0.035) 1px, transparent 1px) 0 0 / 48px 48px,
    linear-gradient(rgba(20, 32, 51, 0.035) 1px, transparent 1px) 0 0 / 48px 48px,
    var(--paper);
  overflow: hidden;
}

.content-shell {
  width: min(1100px, calc(100% - 40px));
  margin: 0 auto;
}

.content-shell--hero {
  width: min(1260px, calc(100% - 40px));
}

.content-shell--wide {
  width: min(1240px, calc(100% - 40px));
}

.side-rail {
  position: fixed;
  top: 50%;
  left: 22px;
  z-index: 18;
  display: grid;
  gap: 8px;
  padding: 8px;
  border: 1px solid var(--line);
  border-radius: 8px;
  background: rgba(255, 255, 255, 0.78);
  box-shadow: 0 18px 42px rgba(20, 32, 51, 0.11);
  backdrop-filter: blur(18px);
  transform: translateY(-50%);
}

.side-rail a {
  position: relative;
  display: grid;
  width: 40px;
  height: 40px;
  place-items: center;
  border-radius: 7px;
  color: var(--muted-ink);
  transition: color 180ms ease, background 180ms ease, transform 180ms ease;
}

.side-rail a:hover,
.side-rail a:focus-visible {
  border-bottom: 0;
  color: var(--page-ink);
  background: var(--cyan-soft);
  transform: translateX(1px);
}

.side-rail .el-icon {
  width: 28px;
  height: 28px;
  border-radius: 7px;
  color: var(--cyan);
  background: #f4fbfb;
}

.side-rail span {
  position: absolute;
  left: 50px;
  top: 50%;
  min-width: 72px;
  padding: 8px 10px;
  border: 1px solid var(--line);
  border-radius: 7px;
  color: var(--page-ink);
  background: rgba(255, 255, 255, 0.96);
  box-shadow: 0 12px 26px rgba(20, 32, 51, 0.12);
  font-family: "DemiFont", Arial, sans-serif;
  font-size: 12px;
  line-height: 1;
  letter-spacing: 0;
  opacity: 0;
  pointer-events: none;
  transform: translate(4px, -50%);
  transition: opacity 160ms ease, transform 160ms ease;
  white-space: nowrap;
}

.side-rail a:hover span,
.side-rail a:focus-visible span {
  opacity: 1;
  transform: translate(0, -50%);
}

.hero-section {
  position: relative;
  padding: 58px 0 74px;
  overflow: hidden;
}

.hero-grid {
  position: absolute;
  inset: 0;
  pointer-events: none;
  background:
    linear-gradient(90deg, rgba(20, 32, 51, 0.04) 1px, transparent 1px) 0 0 / 56px 56px,
    linear-gradient(rgba(20, 32, 51, 0.04) 1px, transparent 1px) 0 0 / 56px 56px,
    linear-gradient(180deg, #f7fbfa 0%, #ffffff 68%, #f7faf9 100%);
}

.hero-grid::after {
  position: absolute;
  inset: 0;
  content: "";
  background:
    linear-gradient(90deg, rgba(247, 251, 250, 0.28), rgba(255, 255, 255, 0.92) 52%, rgba(247, 251, 250, 0.28));
}

.hero-copy,
.hero-showcase,
.overview-grid {
  position: relative;
  z-index: 1;
}

.hero-copy {
  display: grid;
  justify-items: center;
  text-align: center;
}

.project-title {
  width: min(1100px, 100%);
  margin: 0 auto;
  color: #101a2b;
  font-family: "BoldFont", Times, "Times New Roman", serif;
  font-size: 50px;
  line-height: 1.08;
  letter-spacing: 0;
  text-align: center;
}

.hero-showcase {
  width: min(1060px, 100%);
  margin: 34px auto 0;
  padding: 12px;
  border: 1px solid var(--line);
  border-radius: 8px;
  background: rgba(255, 255, 255, 0.9);
  box-shadow: 0 22px 58px rgba(20, 32, 51, 0.12);
  overflow: hidden;
}

.hero-showcase::before {
  position: absolute;
  inset: 0;
  padding: 1px;
  border-radius: inherit;
  background:
    radial-gradient(circle at 0% 0%, transparent 0%, transparent 28%, rgba(11, 131, 146, 0.48) 42%, rgba(39, 121, 90, 0.42) 54%, transparent 68%, transparent 100%);
  background-size: 240% 240%;
  content: "";
  pointer-events: none;
  -webkit-mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
  -webkit-mask-composite: xor;
  mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
  mask-composite: exclude;
  animation: shine 12s linear infinite;
}

.hero-image {
  position: relative;
  display: block;
  width: 100%;
  height: auto;
  border-radius: 6px;
}

.overview-grid {
  width: min(1060px, 100%);
  margin: 28px auto 0;
}

.abstract-copy {
  margin: 0;
  padding: 22px 24px;
  border: 1px solid var(--line);
  border-left: 4px solid var(--cyan);
  border-radius: 8px;
  color: #334052;
  background: rgba(255, 255, 255, 0.8);
  box-shadow: 0 16px 40px rgba(20, 32, 51, 0.08);
  font-size: 18px;
  line-height: 1.72;
  text-align: justify;
}

.paper-section {
  position: relative;
  padding: 82px 0 88px;
  border-top: 1px solid var(--line);
}

.paper-section--light {
  background:
    linear-gradient(180deg, #ffffff 0%, #f7faf9 100%);
}

.paper-section--tint {
  background:
    linear-gradient(180deg, #f3fbfb 0%, #ffffff 100%);
}

.section-heading {
  max-width: 900px;
  margin: 0 auto 28px;
  text-align: center;
}

.section-heading h2 {
  color: var(--page-ink);
  font-family: "BoldFont", Times, "Times New Roman", serif;
  font-size: 42px;
  line-height: 1.08;
  letter-spacing: 0;
  text-align: center;
}

.section-copy {
  max-width: 1000px;
  margin: 0 auto 32px;
  color: #334052;
  font-size: 18px;
  line-height: 1.72;
  text-align: justify;
}

.media-grid {
  display: grid;
  gap: 20px;
  align-items: start;
}

.media-grid--two {
  grid-template-columns: repeat(2, minmax(0, 1fr));
}

.media-card {
  position: relative;
  margin: 0;
  padding: 10px;
  border: 1px solid var(--line);
  border-radius: 8px;
  background:
    linear-gradient(180deg, rgba(255, 255, 255, 0.94), rgba(248, 252, 251, 0.86));
  box-shadow: 0 18px 48px rgba(20, 32, 51, 0.12);
  overflow: hidden;
  transition: border-color 180ms ease, transform 180ms ease, box-shadow 180ms ease;
}

.media-card:hover {
  border-color: rgba(11, 131, 146, 0.3);
  box-shadow: 0 24px 62px rgba(20, 32, 51, 0.15);
  transform: translateY(-2px);
}

.media-card--tracking {
  width: min(820px, 100%);
  margin: 0 auto;
}

.media-meta {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 12px;
  min-height: 42px;
  padding: 0 4px 10px;
}

.media-meta span {
  flex: 0 0 auto;
  color: var(--cyan);
  font-family: "DemiFont", Arial, sans-serif;
  font-size: 13px;
  line-height: 1.3;
}

.media-meta strong {
  color: var(--page-ink);
  font-family: "DemiFont", Arial, sans-serif;
  font-size: 15px;
  line-height: 1.35;
  letter-spacing: 0;
  text-align: right;
}

.media-image {
  display: block;
  width: 100%;
  height: auto;
  margin-bottom: 12px;
  border: 1px solid rgba(20, 32, 51, 0.09);
  border-radius: 6px;
  background: #ffffff;
}

.media-frame {
  position: relative;
  overflow: hidden;
  border-radius: 6px;
  background: #0f1724;
}

.media-frame::after {
  position: absolute;
  inset: 0;
  border: 1px solid rgba(255, 255, 255, 0.16);
  border-radius: inherit;
  content: "";
  pointer-events: none;
}

.media-frame--letter {
  aspect-ratio: 3006 / 1080;
}

.media-frame--wide {
  aspect-ratio: 16 / 9;
}

.media-video {
  display: block;
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.media-video--contain {
  object-fit: contain;
  background: #ffffff;
}

.control-panel {
  display: grid;
  grid-template-columns: auto minmax(260px, 1fr) auto;
  gap: 12px;
  align-items: center;
  width: min(760px, 100%);
  margin: 28px auto 0;
  padding: 10px;
  border: 1px solid var(--line);
  border-radius: 8px;
  background:
    linear-gradient(180deg, rgba(255, 255, 255, 0.94), rgba(248, 252, 251, 0.86));
  box-shadow: 0 18px 42px rgba(20, 32, 51, 0.1);
  backdrop-filter: blur(16px);
}

.speed-label {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  min-height: 42px;
  width: 196px;
  padding: 0 14px;
  border: 1px solid rgba(20, 32, 51, 0.08);
  border-radius: 8px;
  color: #263344;
  background: rgba(255, 255, 255, 0.75);
  font-family: "DemiFont", Arial, sans-serif;
  font-size: 15px;
  font-variant-numeric: tabular-nums;
  line-height: 1.4;
  text-align: center;
  white-space: nowrap;
}

.speed-slider {
  min-width: 240px;
  padding: 0 16px 10px;
}

.project-page :deep(.el-slider) {
  --el-slider-main-bg-color: transparent;
  --el-slider-runway-bg-color: transparent;
  --el-slider-stop-bg-color: rgba(255, 255, 255, 0.95);
  --el-slider-button-size: 20px;
}

.project-page :deep(.el-slider__runway) {
  height: 8px;
  border: 1px solid rgba(20, 32, 51, 0.08);
  border-radius: 999px;
  background:
    linear-gradient(90deg, rgba(11, 131, 146, 0.1), rgba(39, 121, 90, 0.1)),
    #eef4f3;
  box-shadow: inset 0 1px 2px rgba(20, 32, 51, 0.08);
  cursor: pointer;
  transition: background 180ms ease, box-shadow 180ms ease;
}

.project-page :deep(.el-slider__bar) {
  height: 8px;
  border-radius: 999px;
  background: linear-gradient(90deg, var(--cyan), var(--green));
  box-shadow: 0 7px 18px rgba(11, 131, 146, 0.2);
  transition: width 140ms cubic-bezier(0.22, 1, 0.36, 1);
  will-change: width;
}

.project-page :deep(.el-slider__button-wrapper) {
  transition: left 140ms cubic-bezier(0.22, 1, 0.36, 1);
  will-change: left;
}

.project-page :deep(.el-slider__button) {
  width: 20px;
  height: 20px;
  border: 4px solid #ffffff;
  background: var(--cyan);
  box-shadow:
    0 0 0 1px rgba(11, 131, 146, 0.35),
    0 8px 18px rgba(20, 32, 51, 0.18);
  transition: transform 160ms ease, box-shadow 160ms ease, background 160ms ease;
}

.project-page :deep(.el-slider__button:hover),
.project-page :deep(.el-slider__button.hover),
.project-page :deep(.el-slider__button.dragging) {
  background: #087586;
  box-shadow:
    0 0 0 5px rgba(11, 131, 146, 0.1),
    0 10px 24px rgba(20, 32, 51, 0.2);
  transform: scale(1.08);
}

.project-page :deep(.el-slider__marks-text) {
  color: var(--muted-ink);
  font-family: "DemiFont", Arial, sans-serif;
  font-size: 12px;
  letter-spacing: 0;
}

.project-page :deep(.el-slider__stop) {
  width: 4px;
  height: 4px;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.95);
  box-shadow: 0 0 0 1px rgba(20, 32, 51, 0.08);
}

.project-page :deep(.el-button.custom-button) {
  position: relative;
  min-height: 42px;
  padding: 0 17px;
  border: 1px solid rgba(255, 255, 255, 0.26);
  border-radius: 8px;
  background:
    linear-gradient(135deg, #142033 0%, #0b6471 100%);
  font-family: "DemiFont", Arial, sans-serif;
  font-size: 15px;
  font-weight: 700;
  letter-spacing: 0;
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.16),
    0 12px 24px rgba(20, 32, 51, 0.18);
  overflow: hidden;
}

.project-page :deep(.el-button.custom-button::before) {
  position: absolute;
  inset: 0;
  background:
    linear-gradient(110deg, transparent 0%, rgba(255, 255, 255, 0.22) 46%, transparent 72%);
  content: "";
  opacity: 0;
  transform: translateX(-70%);
  transition: opacity 180ms ease, transform 360ms ease;
}

.project-page :deep(.el-button.custom-button:hover),
.project-page :deep(.el-button.custom-button:focus) {
  background:
    linear-gradient(135deg, #102033 0%, var(--cyan) 100%);
  transform: translateY(-1px);
}

.project-page :deep(.el-button.custom-button:hover::before),
.project-page :deep(.el-button.custom-button:focus::before) {
  opacity: 1;
  transform: translateX(70%);
}

@keyframes shine {
  0% {
    background-position: 0% 0%;
  }

  50% {
    background-position: 100% 100%;
  }

  100% {
    background-position: 0% 0%;
  }
}

@media (max-width: 1180px) {
  .side-rail {
    display: none;
  }
}

@media (max-width: 1080px) {
  .project-title {
    font-size: 42px;
  }

}

@media (max-width: 820px) {
  .media-grid,
  .media-grid--two {
    grid-template-columns: 1fr;
  }

  .control-panel {
    grid-template-columns: 1fr;
  }

  .speed-label {
    width: 100%;
  }

  .speed-slider {
    min-width: 0;
    width: 100%;
  }
}

@media (max-width: 720px) {
  .content-shell,
  .content-shell--hero,
  .content-shell--wide {
    width: min(100% - 28px, 640px);
  }

  .hero-section {
    padding: 42px 0 56px;
  }

  .paper-section {
    padding: 58px 0 64px;
  }

  .project-title {
    font-size: 34px;
    line-height: 1.1;
  }

  .section-heading h2 {
    font-size: 31px;
  }

  .abstract-copy,
  .section-copy {
    font-size: 17px;
    line-height: 1.66;
    text-align: left;
  }

  .abstract-copy {
    padding: 18px;
  }

  .media-meta {
    align-items: flex-start;
    flex-direction: column;
    gap: 4px;
  }

  .media-meta strong {
    text-align: left;
  }
}

@media (max-width: 460px) {
  .project-title {
    font-size: 29px;
  }
}

@media (prefers-reduced-motion: reduce) {
  .hero-showcase::before {
    animation: none;
  }

  .side-rail a,
  .media-card,
  .project-page :deep(.el-slider__bar),
  .project-page :deep(.el-slider__button-wrapper),
  .project-page :deep(.el-slider__button),
  .project-page :deep(.el-button.custom-button::before) {
    transition: none;
  }
}
</style>
