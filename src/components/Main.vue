<script setup>
import { nextTick, onMounted, ref, watch } from 'vue'
import { RefreshRight } from '@element-plus/icons-vue'

const baseUrl = import.meta.env.BASE_URL
const letterSpeed = ref(1)
const realWorldSpeed = ref(1)
const trackingSpeed = ref(1)

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
    label: '12 UAVs',
    wide: true,
  },
  {
    id: 'letter18',
    image: 'icra1_2.png',
    video: 'video/2_final.mp4',
    label: '18 UAVs',
    wide: true,
  },
]

const transitionDemos = [
  {
    id: 'transition-square',
    image: 'line.png',
    video: 'video/traj.mp4',
    label: 'Square to Triangle',
  },
  {
    id: 'transition-line',
    image: 'triangle.png',
    video: 'video/line.mp4',
    label: 'Vertical Line to Horizontal Line',
  },
]

function assetPath(path) {
  return `${baseUrl.replace(/\/?$/, '/')}${path.replace(/^\/+/, '')}`
}

function setVideoSpeed(selector, speed) {
  document.querySelectorAll(selector).forEach(video => {
    video.playbackRate = speed
  })
}

function restartVideos(selector, speed) {
  document.querySelectorAll(selector).forEach(video => {
    video.currentTime = 0
    if (speed) {
      video.playbackRate = speed
    }
    const playPromise = video.play()
    if (playPromise && typeof playPromise.catch === 'function') {
      playPromise.catch(() => {})
    }
  })
}

function formatSpeed(value) {
  return `${value}x`
}

watch(letterSpeed, value => {
  nextTick(() => setVideoSpeed("video[data-group='letter']", value))
})

watch(realWorldSpeed, value => {
  nextTick(() => setVideoSpeed("video[data-group='real-world']", value))
})

watch(trackingSpeed, value => {
  nextTick(() => setVideoSpeed("video[data-group='tracking']", value))
})

onMounted(() => {
  setVideoSpeed("video[data-group='letter']", letterSpeed.value)
  setVideoSpeed("video[data-group='real-world']", realWorldSpeed.value)
  setVideoSpeed("video[data-group='tracking']", trackingSpeed.value)
})
</script>

<template>
  <main class="project-page">
    <section class="hero-section">
      <div class="content-shell content-shell--hero">
        <h1 class="project-title">
          Graph-Based Multi-Agent Reinforcement Learning for Scalable UAV Formation Control and Target Tracking
        </h1>

        <figure class="hero-figure">
          <img :src="assetPath('framework_gnn_2.png')" alt="Framework overview" class="hero-image" />
        </figure>

        <p class="abstract-copy">
          This paper presents a graph-based multi-agent reinforcement learning framework for scalable UAV formation control and target tracking. The framework introduces a conflict-aware graph representation that aggregates neighborhood information through attention-based message passing, enabling each UAV to analyze both local interactions and global formation geometry. To generate agile and stable maneuvers, a hierarchical policy is designed that first selects motion primitives from a structured library and then refines them with continuous trajectory adjustments, ensuring smooth and dynamically feasible flight in cluttered environments. Extensive simulations and real-world experiments validate the proposed approach, demonstrating accurate target tracking, stable formation maintenance, and robust adaptation across varying swarm sizes and obstacle densities. In particular, policies trained on smaller swarms generalize effectively to larger ones without retraining, highlighting the scalability and practicality.
        </p>
      </div>
    </section>

    <section class="paper-section">
      <div class="content-shell content-shell--wide">
        <div class="section-heading">
          <h2>Letter Formation Demo</h2>
        </div>
        <p class="section-copy">
          This experiment demonstrates a UAV swarm performing dynamic formation transitions while tracking a moving target. The red dot with a dashed line indicates the target trajectory, while the colored curves show UAV flight paths, with color gradients representing temporal evolution. Gray cylinders denote obstacles, and the horizontal time bar illustrates the progression of formation changes. During the experiment, the swarm successfully forms the letters “ICRA”, maintaining stable coordination and precise target following even in cluttered environments.
        </p>

        <div class="media-grid media-grid--two">
          <figure v-for="demo in letterDemos" :key="demo.id" class="media-card media-card--letter">
            <img :src="assetPath(demo.image)" :alt="demo.label" class="media-image" />
            <div class="media-frame media-frame--wide">
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
            <figcaption>{{ demo.label }}</figcaption>
          </figure>
        </div>

        <div class="control-panel control-panel--speed">
          <span class="speed-label">Playback Speed: {{ letterSpeed }}x</span>
          <div class="speed-slider">
            <el-slider v-model="letterSpeed" :min="0.5" :max="2" :step="0.1" :marks="speedMarks" :format-tooltip="formatSpeed" />
          </div>
          <el-button
            type="primary"
            :icon="RefreshRight"
            class="custom-button"
            @click="restartVideos(`video[data-group='letter']`, letterSpeed)"
          >
            Restart Videos
          </el-button>
        </div>
      </div>
    </section>

    <section class="paper-section paper-section--alt">
      <div class="content-shell content-shell--wide">
        <div class="section-heading">
          <h2>Formation Transition</h2>
        </div>
        <p class="section-copy">
          We tested our method on four Crazyflie 2.0 drones in an indoor space with obstacles. The drones and the target car were tracked using the HTC Vive system, and a Livox LiDAR was used to build a 3D map of the environment. The drones had to follow the moving car while keeping formation and smoothly changing their shape when needed. We tested two formation switches: from square to triangle, and from vertical line to horizontal line.
        </p>

        <div class="media-grid media-grid--two">
          <figure v-for="demo in transitionDemos" :key="demo.id" class="media-card">
            <img :src="assetPath(demo.image)" :alt="demo.label" class="media-image" />
            <div class="media-frame media-frame--video">
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
            <figcaption>{{ demo.label }}</figcaption>
          </figure>
        </div>

        <div class="control-panel control-panel--speed">
          <span class="speed-label">Playback Speed: {{ realWorldSpeed }}x</span>
          <div class="speed-slider">
            <el-slider v-model="realWorldSpeed" :min="0.5" :max="2" :step="0.1" :marks="speedMarks" :format-tooltip="formatSpeed" />
          </div>
          <el-button
            type="primary"
            :icon="RefreshRight"
            class="custom-button"
            @click="restartVideos(`video[data-group='real-world']`, realWorldSpeed)"
          >
            Restart Videos
          </el-button>
        </div>
      </div>
    </section>

    <section class="paper-section">
      <div class="content-shell">
        <div class="section-heading">
          <h2>Target Tracking</h2>
        </div>
        <p class="section-copy">
          A team of UAVs was required to maintain a trapezoid formation while following a moving ground target in an environment filled with obstacles. The swarm demonstrated the ability to preserve the trapezoid shape, avoid collisions, and adapt its collective motion to environmental constraints.
        </p>

        <figure class="media-card media-card--tracking">
          <div class="media-frame media-frame--video">
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
          <span class="speed-label">Playback Speed: {{ trackingSpeed }}x</span>
          <div class="speed-slider">
            <el-slider v-model="trackingSpeed" :min="0.5" :max="2" :step="0.1" :marks="speedMarks" :format-tooltip="formatSpeed" />
          </div>
          <el-button
            type="primary"
            :icon="RefreshRight"
            class="custom-button"
            @click="restartVideos(`video[data-group='tracking']`, trackingSpeed)"
          >
            Restart Videos
          </el-button>
        </div>
      </div>
    </section>
  </main>
</template>

<style scoped>
.project-page {
  --page-ink: #142033;
  --muted-ink: #5b6678;
  --paper: #f8fbff;
  --panel: #ffffff;
  --panel-soft: #eef6ff;
  --line: #d7e5f2;
  --accent: #2f7fb8;
  --accent-dark: #1f5f8f;
  --warm: #5d95c8;
  background: var(--paper);
  color: var(--page-ink);
  min-height: 100vh;
}

.content-shell {
  margin: 0 auto;
  width: min(1080px, calc(100% - 40px));
}

.content-shell--hero {
  width: min(1160px, calc(100% - 40px));
}

.content-shell--wide {
  width: min(1220px, calc(100% - 40px));
}

.hero-section {
  background: #edf7ff;
  border-bottom: 1px solid var(--line);
  padding: 54px 0 58px;
}

.project-title {
  color: #111b2b;
  font-family: "BoldFont", Times, "Times New Roman", serif;
  font-size: 42px;
  line-height: 1.16;
  margin: 0 auto;
  max-width: 1040px;
  text-align: center;
}

.hero-figure {
  background: var(--panel);
  border: 1px solid #c9dcec;
  border-radius: 8px;
  box-shadow: 0 18px 42px rgba(31, 95, 143, 0.12);
  margin: 34px auto 0;
  max-width: 980px;
  overflow: hidden;
}

.hero-image {
  display: block;
  height: auto;
  width: 100%;
}

.abstract-copy {
  border-left: 4px solid var(--warm);
  color: #263344;
  font-size: 19px;
  line-height: 1.72;
  margin: 28px auto 0;
  max-width: 980px;
  padding-left: 20px;
  text-align: justify;
}

.paper-section {
  background: var(--paper);
  border-bottom: 1px solid var(--line);
  padding: 58px 0 62px;
}

.paper-section--alt {
  background: var(--panel-soft);
}

.section-heading {
  margin: 0 auto 24px;
  max-width: 900px;
}

.section-heading h2 {
  color: var(--page-ink);
  font-family: "BoldFont", Times, "Times New Roman", serif;
  font-size: 30px;
  line-height: 1.22;
  margin: 0;
  text-align: center;
}

.section-copy {
  color: #2f3b4d;
  font-size: 18px;
  line-height: 1.72;
  margin: 0 auto 28px;
  max-width: 1000px;
  text-align: justify;
}

.media-grid {
  align-items: start;
  display: grid;
  gap: 22px;
  margin: 0 auto;
  max-width: 1000px;
}

.media-grid--two {
  grid-template-columns: repeat(2, minmax(0, 1fr));
}

.media-card {
  background: var(--panel);
  border: 1px solid var(--line);
  border-radius: 8px;
  box-shadow: 0 10px 26px rgba(31, 95, 143, 0.08);
  margin: 0;
  overflow: hidden;
  padding: 10px;
}

.media-card--tracking {
  margin: 0 auto;
  max-width: 680px;
}

.media-image {
  background: #fff;
  border: 1px solid var(--line);
  border-radius: 6px;
  display: block;
  height: auto;
  margin-bottom: 12px;
  width: 100%;
}

.media-frame {
  background: #0f1724;
  border-radius: 6px;
  overflow: hidden;
}

.media-frame--video {
  aspect-ratio: 16 / 9;
}

.media-frame--wide {
  background: #ffffff;
}

.media-video {
  display: block;
  height: 100%;
  object-fit: cover;
  width: 100%;
}

.media-video--contain {
  height: auto;
  object-fit: contain;
}

figcaption {
  color: var(--muted-ink);
  font-family: "DemiFont", Arial, sans-serif;
  font-size: 15px;
  line-height: 1.45;
  margin-top: 10px;
  min-height: 22px;
  text-align: center;
}

.control-panel {
  align-items: center;
  background: rgba(255, 255, 255, 0.86);
  border: 1px solid var(--line);
  border-radius: 8px;
  box-shadow: 0 8px 22px rgba(31, 95, 143, 0.07);
  display: flex;
  gap: 18px;
  justify-content: center;
  margin: 26px auto 0;
  max-width: 100%;
  padding: 12px 16px;
  width: fit-content;
}

.control-panel--speed {
  flex-wrap: wrap;
  width: min(780px, 100%);
}

.speed-label {
  color: #263344;
  flex: 0 0 auto;
  font-family: "DemiFont", Arial, sans-serif;
  font-size: 16px;
  line-height: 1.4;
  min-width: 180px;
  text-align: right;
  white-space: nowrap;
}

.speed-slider {
  flex: 1 1 310px;
  max-width: 360px;
  min-width: 240px;
  padding: 0 8px;
}

.project-page :deep(.el-slider__runway) {
  background-color: #d9e9f7;
}

.project-page :deep(.el-slider__bar) {
  background-color: var(--accent);
}

.project-page :deep(.el-slider__button) {
  border-color: var(--accent);
}

.project-page :deep(.el-slider__marks-text) {
  color: var(--muted-ink);
  font-family: "DemiFont", Arial, sans-serif;
  font-size: 12px;
}

.project-page :deep(.el-button.custom-button) {
  background: var(--accent);
  border: 0;
  border-radius: 6px;
  font-family: "DemiFont", Arial, sans-serif;
  font-size: 15px;
  font-weight: 700;
  letter-spacing: 0;
  min-height: 40px;
}

.project-page :deep(.el-button.custom-button:hover),
.project-page :deep(.el-button.custom-button:focus) {
  background: var(--accent-dark);
}

@media (max-width: 980px) {
  .project-title {
    font-size: 36px;
  }

}

@media (max-width: 720px) {
  .content-shell,
  .content-shell--hero,
  .content-shell--wide {
    width: min(calc(100% - 28px), 640px);
  }

  .hero-section {
    padding: 38px 0 44px;
  }

  .paper-section {
    padding: 44px 0 48px;
  }

  .project-title {
    font-size: 30px;
    line-height: 1.2;
  }

  .section-heading h2 {
    font-size: 26px;
  }

  .abstract-copy,
  .section-copy {
    font-size: 17px;
    line-height: 1.66;
    text-align: left;
  }

  .abstract-copy {
    padding-left: 16px;
  }

  .media-grid,
  .media-grid--two {
    grid-template-columns: 1fr;
  }

  .media-card {
    padding: 8px;
  }

  .control-panel {
    width: 100%;
  }

  .control-panel--speed {
    align-items: stretch;
  }

  .speed-label {
    min-width: 0;
    text-align: center;
    width: 100%;
  }

  .speed-slider {
    max-width: none;
    min-width: 0;
    width: 100%;
  }
}

@media (max-width: 420px) {
  .project-title {
    font-size: 27px;
  }
}
</style>
