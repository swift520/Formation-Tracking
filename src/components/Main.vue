<script setup>

function restartObstacleVideos() {
  const obstacleVideos = document.querySelectorAll("video[data-key*='obs']");
  obstacleVideos.forEach(video => {
    video.currentTime = 0;
    video.play();
  });
}

function restartSpeedVideos() {
  const speedVideos = document.querySelectorAll("video[data-key*='vel']");
  speedVideos.forEach(video => {
    video.currentTime = 0;
    video.play();
  });
}

function setVideosToStopAtLastFrame() {
  const videos = document.querySelectorAll("video");
  videos.forEach(video => {
    video.addEventListener("ended", () => {
      video.currentTime = video.duration - 0.01; // Set to the last frame
    });
  });
}

</script>


<template>
  <div style="height: 48px;"></div>
    <el-row justify="center" style="margin-bottom: 36px;">
      <el-col :xs="24" :sm="22" :md="22" :lg="20" :xl="16">
        <h1 class="section-title" style="margin-bottom: 28px;">End-to-End Trajectory Planner for Safe Navigation in Crowded Dynamic Environments</h1>
      </el-col>
    </el-row>

  <div>
    <!-- <el-divider /> -->
    <el-row justify="center" style="margin-bottom: 36px;">
        <el-col :xs="24" :sm="20" :md="20" :lg="17" :xl="14">
            <!-- <h1 style="margin-bottom: 20px;">摘要</h1> -->
            <img src="/public/framework.png" alt="Logo" style="width:100%;margin-bottom:12px;border-radius:10px;" />
            <p style="margin-bottom: 16px;">
              This paper presents a novel end-to-end trajectory planner that integrates LiDAR-based  perception and planning into a unified framework, enabling UAVs to navigate efficiently while avoiding obstacles in dynamic environments. 
              Learning-based dynamic planning methods often rely on reinforcement learning, which faces challenges such as low training efficiency, instability, and safety risks due to the iterative action-feedback training loop. To address these limitations, we propose a lightweight map representation for temporally continuous dynamic obstacles and leverage physical information from simulation environments to enable unsupervised network training. By incorporating a repulsion-based adjustment mechanism grounded in motion primitives, the planner adaptively selects planning directions, generating feasible trajectories even in highly crowded scenarios. 
              Extensive simulation and real-world experiments validate the safety and high flight efficiency of the proposed planner, demonstrating its effectiveness.
            </p>
        </el-col>
    </el-row>
  </div>

  <div>
    <el-divider />

    <el-row justify="center">
      <h2 class="section-title" style="margin-bottom: 32px;">Visualization of Trajectories</h2>
    </el-row>

    <el-row justify="center" style="margin-bottom: 56px;">
      <el-col :xs="24" :sm="22" :md="20" :lg="18" :xl="14">

        <el-row justify="center" gutter="20">
          <el-col :xs="12" :sm="12" :md="12" :lg="12" :xl="12" style="display:flex;justify-content:center;">
            <video autoplay loop muted preload playsinline style="width:100%;max-width:650px;aspect-ratio:16/9;border-radius:10px;object-fit:cover;" controlslist="nodownload nofullscreen noremoteplayback noaudio noplaybackrate">
              <source src="/video/0.mp4" type="video/mp4">
            </video>
          </el-col>
          <el-col :xs="12" :sm="12" :md="12" :lg="12" :xl="12" style="display:flex;justify-content:center;">
            <video autoplay loop muted preload playsinline style="width:100%;max-width:650px;aspect-ratio:16/9;border-radius:10px;object-fit:cover;" controlslist="nodownload nofullscreen noremoteplayback noaudio noplaybackrate">
              <source src="/video/1.mp4" type="video/mp4">
            </video>
          </el-col>
        </el-row>

      </el-col>
    </el-row>
  </div>

  <div>
    <el-divider />

    <el-row justify="center">
      <h2 class="section-title" style="margin-bottom: 12px;">Environmental Dynamism Test</h2>
    </el-row>

    <el-row justify="center" style="margin-bottom: 36px;">
      <el-col :xs="24" :sm="22" :md="20" :lg="20" :xl="18">
        <p style="margin-bottom: 24px;">
          Three sets of simulations with varying dynamic obstacle densities were conducted.
          The maximum flight velocity was set to 2.5 m/s and the velocity of dynamic obstacles was limited to 1.25 m/s.
        </p>

        <el-row justify="center" gutter="10">
          <el-col :xs="24" :sm="8" :md="8" :lg="8" :xl="8" style="display:flex;justify-content:center;">
            <div style="display:flex;flex-direction:column;align-items:center;width:100%;">
              <img src="/public/40.png" alt="obs40" style="width:90%;max-width:450px;aspect-ratio:7/5;object-fit:contain;margin-bottom:-18px;" />
              <p> 140 static & 40 dynamic </p>
              <video key='obs40' data-key='obs40' autoplay loop muted preload playsinline style="width:100%;max-width:450px;aspect-ratio:1/1;border-radius:10px;object-fit:cover;" controlslist="nodownload nofullscreen noremoteplayback noaudio noplaybackrate">
                <source src="/video/obs40.mp4" type="video/mp4">
              </video>
            </div>
          </el-col>
          <el-col :xs="24" :sm="8" :md="8" :lg="8" :xl="8" style="display:flex;justify-content:center;">
            <div style="display:flex;flex-direction:column;align-items:center;width:100%;">
              <img src="/public/70.png" alt="obs70" style="width:90%;max-width:450px;aspect-ratio:7/5;object-fit:contain;margin-bottom:-18px;" />
              <p> 100 static & 70 dynamic </p>
              <video key='obs70' data-key='obs70' autoplay loop muted preload playsinline style="width:100%;max-width:450px;aspect-ratio:1/1;border-radius:10px;object-fit:cover;" controlslist="nodownload nofullscreen noremoteplayback noaudio noplaybackrate">
                <source src="/video/obs70.mp4" type="video/mp4">
              </video>
            </div>
          </el-col>
          <el-col :xs="24" :sm="8" :md="8" :lg="8" :xl="8" style="display:flex;justify-content:center;">
            <div style="display:flex;flex-direction:column;align-items:center;width:100%;">
              <img src="/public/100.png" alt="obs100" style="width:90%;max-width:450px;aspect-ratio:7/5;object-fit:contain;margin-bottom:-18px;" />
              <p> 70 static & 100 dynamic </p>
              <video key='obs100' data-key='obs100' autoplay loop muted preload playsinline style="width:100%;max-width:450px;aspect-ratio:1/1;border-radius:10px;object-fit:cover;" controlslist="nodownload nofullscreen noremoteplayback noaudio noplaybackrate">
                <source src="/video/obs100.mp4" type="video/mp4">
              </video>
            </div>
          </el-col>
        </el-row>
        <img src="/public/method.png" alt="obs40" style="width:100%;max-width:700px;object-fit:contain;display:block;margin:auto;" />
        <div style="height: 18px;"></div>
        <el-row justify="center">
          <el-button type="primary" @click="restartObstacleVideos" class="custom-button">Restart Videos</el-button>
        </el-row>
        
      </el-col>
    </el-row>
  </div>

  <div>
    <el-divider />

    <el-row justify="center">
      <h2 class="section-title" style="margin-bottom: 12px;">Dynamic Obstacle Velocity Test</h2>
    </el-row>

    <el-row justify="center" style="margin-bottom: 36px;">
      <el-col :xs="24" :sm="22" :md="20" :lg="20" :xl="18">
        <p style="margin-bottom: 12px;">
          Three sets of simulations with maximum velocity of dynamic obstacles were conducted.
          The maximum flight velocity was set to 3 m/s and the scenario contained 140 static and 40 dynamic obstacles.
        </p>
        <el-row justify="center" gutter="10">
          <el-col :xs="24" :sm="8" :md="8" :lg="8" :xl="8" style="display:flex;justify-content:center;">
            <div style="display:flex;flex-direction:column;align-items:center;width:100%;">
              <p> max velocity: 1.5 m/s </p>
              <video key='vel15' data-key='vel15' autoplay loop muted preload playsinline style="width:100%;max-width:450px;aspect-ratio:1/1;border-radius:10px;object-fit:cover;" controlslist="nodownload nofullscreen noremoteplayback noaudio noplaybackrate">
                <source src="/video/vel1.5.mp4" type="video/mp4">
              </video>
            </div>
          </el-col>
          <el-col :xs="24" :sm="8" :md="8" :lg="8" :xl="8" style="display:flex;justify-content:center;">
            <div style="display:flex;flex-direction:column;align-items:center;width:100%;">
              <p> max velocity: 2.0 m/s </p>
              <video key='vel2' data-key='vel2' autoplay loop muted preload playsinline style="width:100%;max-width:450px;aspect-ratio:1/1;border-radius:10px;object-fit:cover;" controlslist="nodownload nofullscreen noremoteplayback noaudio noplaybackrate">
                <source src="/video/vel2.0.mp4" type="video/mp4">
              </video>
            </div>
          </el-col>
          <el-col :xs="24" :sm="8" :md="8" :lg="8" :xl="8" style="display:flex;justify-content:center;">
            <div style="display:flex;flex-direction:column;align-items:center;width:100%;">
              <p> max velocity: 2.5 m/s </p>
              <video key='vel25' data-key='vel25' autoplay loop muted preload playsinline style="width:100%;max-width:450px;aspect-ratio:1/1;border-radius:10px;object-fit:cover;" controlslist="nodownload nofullscreen noremoteplayback noaudio noplaybackrate">
                <source src="/video/vel2.5.mp4" type="video/mp4">
              </video>
            </div>
          </el-col>
        </el-row>
        <img src="/public/method.png" alt="obs40" style="width:100%;max-width:700px;object-fit:contain;display:block;margin:auto;" />
        <div style="height: 18px;"></div>
        <el-row justify="center">
          <el-button type="primary" @click="restartSpeedVideos" class="custom-button">Restart Videos</el-button>
        </el-row>
      </el-col>
    </el-row>
  </div>

    <div>
    <el-divider />

    <el-row justify="center">
      <h2 class="section-title" style="margin-bottom: 18px;">Real-World Experiments</h2>
    </el-row>

    <!-- <el-row justify="center" style="margin-bottom: 56px;">
      <el-col :xs="24" :sm="22" :md="20" :lg="18" :xl="14">

        <el-row justify="center" gutter="20">
          <el-col :xs="12" :sm="12" :md="12" :lg="12" :xl="12" style="display:flex;justify-content:center;">
            <video autoplay loop muted preload playsinline style="width:100%;max-width:650px;aspect-ratio:16/9;border-radius:10px;object-fit:cover;" controlslist="nodownload nofullscreen noremoteplayback noaudio noplaybackrate">
              <source src="/video/0.mp4" type="video/mp4">
            </video>
          </el-col>
          <el-col :xs="12" :sm="12" :md="12" :lg="12" :xl="12" style="display:flex;justify-content:center;">
            <video autoplay loop muted preload playsinline style="width:100%;max-width:650px;aspect-ratio:16/9;border-radius:10px;object-fit:cover;" controlslist="nodownload nofullscreen noremoteplayback noaudio noplaybackrate">
              <source src="/video/1.mp4" type="video/mp4">
            </video>
          </el-col>
        </el-row>

      </el-col>
    </el-row> -->
  </div>

</template>