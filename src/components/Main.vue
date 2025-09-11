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
        <h1 class="section-title" style="margin-bottom: 28px;">Graph-Based Multi-Agent Reinforcement Learning for Scalable UAV Formation Control and Target Tracking</h1>
      </el-col>
    </el-row>

  <div>
    <!-- <el-divider /> -->
    <el-row justify="center" style="margin-bottom: 36px;">
        <el-col :xs="24" :sm="20" :md="20" :lg="17" :xl="10">
            <!-- <h1 style="margin-bottom: 20px;">摘要</h1> -->
            <img src="/public/framework_gnn_2.png" alt="Logo" style="width:100%;margin-bottom:12px;border-radius:10px;" />
            <p style="margin-bottom: 16px;">
This paper presents a graph-based multi-agent reinforcement learning framework for scalable UAV formation control and target tracking. The framework introduces a conflict-aware graph representation that aggregates neighborhood information through attention-based message passing, enabling each UAV to reason about both local interactions and global formation geometry. To generate agile but stable maneuvers, a hierarchical policy is designed that first selects motion primitives from a structured library and then refines them with continuous trajectory adjustments. This combination ensures smooth and dynamically feasible flight in cluttered environments. The proposed approach is extensively validated through both  simulations and real-world experiments, demonstrating accurate target following, stable formation maintenance, and robust adaptation across varying swarm sizes and obstacle densities. The results highlight the scalability and practicality of the framework for complex multi-UAV missions.
            </p>
        </el-col>
    </el-row>
  </div>

  <div>
    <el-divider />

    <el-row justify="center">
      <h2 class="section-title" style="margin-bottom: 32px;">Letter Formation Demo</h2>
    </el-row>

    <el-row justify="center" style="margin-bottom: 56px;">
      <el-col :xs="24" :sm="22" :md="20" :lg="18" :xl="14">
                <p style="margin-bottom: 24px;">
          This experiment demonstrates a UAV swarm performing dynamic formation transitions while tracking a moving target. The red dot with a dashed line indicates the target trajectory, while the colored curves show UAV flight paths, with color gradients representing temporal evolution. Gray cylinders denote obstacles, and the horizontal time bar illustrates the progression of formation changes. During the experiment, the swarm successfully forms the letters “ICRA”, maintaining stable coordination and precise target following even in cluttered environments.
        </p>

        <el-row justify="center" gutter="20">
            <el-col :xs="12" :sm="12" :md="12" :lg="12" :xl="12" style="display:flex;flex-direction:column;align-items:center;justify-content:center;">
              <img src="/public/icra1_1.png" alt="icra1_1" style="width:100%;max-width:800px;height:auto;border-radius:10px;object-fit:contain;margin-bottom:52px;" />
              <video autoplay loop muted preload playsinline style="width:100%;max-width:800px;aspect-ratio:16/9;border-radius:10px;object-fit:cover;" controlslist="nodownload nofullscreen noremoteplayback noaudio noplaybackrate">
                <source src="/video/1_final.mp4" type="video/mp4">
              </video>
            </el-col>
            <el-col :xs="12" :sm="12" :md="12" :lg="12" :xl="12" style="display:flex;flex-direction:column;align-items:center;justify-content:center;">
              <img src="/public/icra1_2.png" alt="icra1_2" style="width:100%;max-width:800px;height:auto;border-radius:10px;object-fit:contain;margin-bottom:52px;" />
              <video autoplay loop muted preload playsinline style="width:100%;max-width:800px;aspect-ratio:16/9;border-radius:10px;object-fit:cover;" controlslist="nodownload nofullscreen noremoteplayback noaudio noplaybackrate">
                <source src="/video/2_final.mp4" type="video/mp4">
              </video>
            </el-col>
        </el-row>

      </el-col>
    </el-row>
  </div>

  <div>
    <el-divider />

    <el-row justify="center">
      <h2 class="section-title" style="margin-bottom: 32px;">Real-World Formation Transition</h2>
    </el-row>
    <el-row justify="center" style="margin-bottom: 56px;">
      <el-col :xs="24" :sm="22" :md="20" :lg="20" :xl="14">
        <p style="margin-bottom: 24px;">
     We tested our method on four Crazyflie 2.0 drones in an indoor space with obstacles. The drones and the target car were tracked using the HTC Vive system, and a Livox LiDAR was used to build a 3D map of the environment. The drones had to follow the moving car while keeping formation and smoothly changing their shape when needed. We tested two formation switches: from square to triangle, and from vertical line to horizontal line.
        </p>
        <el-row justify="center" gutter="10">
            <el-col :xs="12" :sm="12" :md="12" :lg="12" :xl="12" style="display:flex;flex-direction:column;align-items:center;justify-content:center;">
              <img src="/public/line.png" alt="obs40" style="width:100%;max-width:800px;height:auto;border-radius:10px;object-fit:contain;margin-bottom:52px;" />
              <video key='obs40' data-key='obs40' autoplay loop muted preload playsinline style="width:100%;max-width:800px;aspect-ratio:16/9;border-radius:10px;object-fit:cover;" controlslist="nodownload nofullscreen noremoteplayback noaudio noplaybackrate">
                <source src="/video/traj.mp4" type="video/mp4">
              </video>
              <p style="margin-top:12px;">Square to Triangle</p>
            </el-col>
            <el-col :xs="12" :sm="12" :md="12" :lg="12" :xl="12" style="display:flex;flex-direction:column;align-items:center;justify-content:center;">
              <img src="/public/triangle.png" alt="obs70" style="width:100%;max-width:800px;height:auto;border-radius:10px;object-fit:contain;margin-bottom:52px;" />
              <video key='obs70' data-key='obs70' autoplay loop muted preload playsinline style="width:100%;max-width:800px;aspect-ratio:16/9;border-radius:10px;object-fit:cover;" controlslist="nodownload nofullscreen noremoteplayback noaudio noplaybackrate">
                <source src="/video/line.mp4" type="video/mp4">
              </video>
              <p style="margin-top:12px;">Vertical Line to Horizontal Line</p>
            </el-col>
        </el-row>
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
      <h2 class="section-title" style="margin-bottom: 12px;">Real-World Traget Tracking</h2>
    </el-row>
    <el-row justify="center" style="margin-bottom: 36px;">
      <el-col :xs="24" :sm="22" :md="20" :lg="20" :xl="14">
        <p style="margin-bottom: 24px;">
      A team of UAVs was required to maintain a trapezoid formation while following a moving ground target in an environment filled with obstacles. The swarm demonstrated the ability to preserve the trapezoid shape, avoid collisions, and adapt its collective motion to environmental constraints.
        </p>
        <el-row justify="center" gutter="10">
            <el-col :xs="12" :sm="12" :md="12" :lg="12" :xl="12" style="display:flex;flex-direction:column;align-items:center;justify-content:center;">
              <video key='vel70' data-key='vel70' autoplay loop muted preload playsinline style="width:100%;max-width:800px;aspect-ratio:16/9;border-radius:10px;object-fit:cover;" controlslist="nodownload nofullscreen noremoteplayback noaudio noplaybackrate">
                <source src="/video/trac.mp4" type="video/mp4">
              </video>
            </el-col>
        </el-row>
        <div style="height: 18px;"></div>
        <el-row justify="center">
          <el-button type="primary" @click="restartSpeedVideos" class="custom-button">Restart Videos</el-button>
        </el-row>
        
      </el-col>
    </el-row>
  </div>

</template>