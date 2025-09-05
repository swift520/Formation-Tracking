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
        <el-col :xs="24" :sm="20" :md="20" :lg="17" :xl="8">
            <!-- <h1 style="margin-bottom: 20px;">摘要</h1> -->
            <img src="/public/framework_gnn_2.png" alt="Logo" style="width:100%;margin-bottom:12px;border-radius:10px;" />
            <p style="margin-bottom: 16px;">
          Unmanned Aerial Vehicle (UAV) swarms hold significant promise for surveillance, monitoring, and search-and-rescue, where maintaining formations while tracking moving targets in cluttered environments remains a key challenge. Traditional model-based approaches often struggle with adaptability and scalability, while existing learning-based methods frequently overlook geometric formation constraints. In this paper, we present a scalable graph-based multi-agent reinforcement learning (MARL) framework that unifies formation control and target tracking. Our method represents UAV observations as graphs and employs attention-based message passing to enable decentralized, permutation-invariant coordination. A differentiable gradient-guided formation similarity metric provides explicit geometric feedback, while a hierarchical parameterized action space integrates discrete motion primitives with continuous refinements for dynamically feasible maneuvers. Extensive simulations across varying swarm sizes and obstacle densities demonstrate superior tracking accuracy, formation stability, and generalization compared to state-of-the-art baselines. Real-world experiments  further validate the robustness and practicality of the proposed framework, highlighting its potential for deployment in complex environments. 
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
          Demonstration of UAV swarm formation. The swarm dynamically forms “ICRA” using 12 and 18 UAVs respectively.
        </p>

        <el-row justify="center" gutter="20">
            <el-col :xs="12" :sm="12" :md="12" :lg="12" :xl="12" style="display:flex;flex-direction:column;align-items:center;justify-content:center;">
              <img src="/public/icra1_1.png" alt="icra1_1" style="width:100%;max-width:650px;height:auto;border-radius:10px;object-fit:contain;margin-bottom:52px;" />
              <video autoplay loop muted preload playsinline style="width:100%;max-width:650px;aspect-ratio:16/9;border-radius:10px;object-fit:cover;" controlslist="nodownload nofullscreen noremoteplayback noaudio noplaybackrate">
                <source src="/video/1_final.mp4" type="video/mp4">
              </video>
            </el-col>
            <el-col :xs="12" :sm="12" :md="12" :lg="12" :xl="12" style="display:flex;flex-direction:column;align-items:center;justify-content:center;">
              <img src="/public/icra1_2.png" alt="icra1_2" style="width:100%;max-width:650px;height:auto;border-radius:10px;object-fit:contain;margin-bottom:52px;" />
              <video autoplay loop muted preload playsinline style="width:100%;max-width:650px;aspect-ratio:16/9;border-radius:10px;object-fit:cover;" controlslist="nodownload nofullscreen noremoteplayback noaudio noplaybackrate">
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
      We validated our algorithm on a physical testbed of four Crazyflie UAVs with precise tracking provided by the HTC Vive Lighthouse system. The UAVs were tasked to follow a moving ground vehicle through an obstacle-rich environment while maintaining and reconfiguring their formation. Two transition scenarios were tested: square-to-triangle and vertical-to-horizontal line.
        </p>
        <el-row justify="center" gutter="10">
            <el-col :xs="12" :sm="12" :md="12" :lg="12" :xl="12" style="display:flex;flex-direction:column;align-items:center;justify-content:center;">
              <img src="/public/line.png" alt="obs40" style="width:100%;max-width:650px;height:auto;border-radius:10px;object-fit:contain;margin-bottom:52px;" />
              <video key='obs40' data-key='obs40' autoplay loop muted preload playsinline style="width:100%;max-width:650px;aspect-ratio:16/9;border-radius:10px;object-fit:cover;" controlslist="nodownload nofullscreen noremoteplayback noaudio noplaybackrate">
                <source src="/video/traj.mp4" type="video/mp4">
              </video>
              <p style="margin-top:12px;">Square to Triangle</p>
            </el-col>
            <el-col :xs="12" :sm="12" :md="12" :lg="12" :xl="12" style="display:flex;flex-direction:column;align-items:center;justify-content:center;">
              <img src="/public/triangle.png" alt="obs70" style="width:100%;max-width:650px;height:auto;border-radius:10px;object-fit:contain;margin-bottom:52px;" />
              <video key='obs70' data-key='obs70' autoplay loop muted preload playsinline style="width:100%;max-width:650px;aspect-ratio:16/9;border-radius:10px;object-fit:cover;" controlslist="nodownload nofullscreen noremoteplayback noaudio noplaybackrate">
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
      <el-col :xs="24" :sm="22" :md="20" :lg="20" :xl="18">
        <p style="margin-bottom: 24px;">
      A team of UAVs was required to maintain a trapezoid formation while following a moving ground target in an environment filled with obstacles. The swarm demonstrated the ability to preserve the trapezoid shape, avoid collisions, and adapt its collective motion to environmental constraints.
        </p>
        <el-row justify="center" gutter="10">
            <el-col :xs="12" :sm="12" :md="12" :lg="12" :xl="12" style="display:flex;flex-direction:column;align-items:center;justify-content:center;">
              <video key='vel70' data-key='vel70' autoplay loop muted preload playsinline style="width:100%;max-width:650px;aspect-ratio:16/9;border-radius:10px;object-fit:cover;" controlslist="nodownload nofullscreen noremoteplayback noaudio noplaybackrate">
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