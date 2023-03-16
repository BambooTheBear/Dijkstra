<script setup>
import GapWord from "./GapWord.vue"

</script>

<template>
  {{ points }}
  <br>
  <div style="text-align: left; place-items: left;" class="border-slate-300 border-4 rounded-lg">
    <pre>
      <code>
      <span class="keyword">import</span> java.util.ArrayList;
      <br>
      <span class="keyword">public class</span> Main {
      <br>
        <span class="keyword">abstract class</span> Graph {
          <br>
            <span class="comment">  // Returns the number of nodes in the graph</span>
            <br>
            <span class="keyword">  abstract</span> int nodeCount();
            <br>
            <span class="comment">  // Returns all nodes connected to </span>
            <br>
            <span class="keyword">  abstract</span> int[] neighboursFrom(int node);
            <br>
            <span class="comment">  // Returns all nodes contained in the graph</span>
            <br>
            <span class="keyword">  abstract</span> ArrayList&lt;Integer&gt; nodes();
            <br>
            <span class="comment">// Calculates the distance between node1 and node2 </span>
            <br>
            <span class="keyword">abstract</span> double distance(int node1, int node2);
            <br>
        }
        </code>
      </pre>
  </div>
  <br>
  <br>
  <div style="text-align: left;" class="border-slate-300 border-4 rounded-lg">
    <pre>
        <code>
        <GapWord :correctWord="'int[]'" @clicked="onChildUpdate"/> dijkstra(<span class="type">Graph</span> graph, <span class="keyword">int</span> startNode) {

          <span class="type">double</span>[] distance = <span class="keyword">new</span> <span class="type">double</span>[graph.<span class="variable">nodeCount</span>()]; <br>
          <span class="keyword">int</span>[] predecessor = <span class="keyword">new</span> <span class="keyword">int</span>[graph.<span class="variable">nodeCount</span>()];<br>
          <span class="type">ArrayList&lt;Integer&gt;</span> notIncluded = <span class="keyword">new</span> <span class="type">ArrayList&lt;&gt;</span>();<br>
          <span class="function-call">initialize</span>(graph, startNode, distance, predecessor, notIncluded);<br>
          <span class="keyword">while</span> (!notIncluded.<span class="function-call">isEmpty</span>()) {<br>
            <span class="keyword">int</span> smallestDistanceNode = notIncluded.<span class="function-call">get</span>(<span class="number">0</span>);<br>
              <span class="keyword">for</span> (<span class="keyword">int</span> currentNode : notIncluded) {<br>
                    <span class="keyword">if</span> (distance[currentNode] &lt; distance[smallestDistanceNode]) {<br>
                        smallestDistanceNode = currentNode;<br>
                        &nbsp;}<br>
                }<br>
                notIncluded.<span class="function-call">remove</span>(smallestDistanceNode);<br>
                <span class="keyword">for</span> (<span class="keyword">int</span> currentNeighbour : graph.<span class="function-call">neighboursFrom</span>(smallestDistanceNode)) {<br>
                  <span class="keyword">if</span> (notIncluded.<span class="function-call">contains</span>(currentNeighbour)) {<br>
                    <span class="function-call">distanceUpdate</span>(graph, smallestDistanceNode, currentNeighbour, distance, predecessor);<br>
                    }<br>
                }<br>
            }<br>
          <span class="keyword">return</span> predecessor;<br>
      }<br>
      </code>
      </pre>
  </div>
  <br>
  <br>
  <div style="text-align: left;" class="border-slate-300 border-4 rounded-lg">
    <pre>
        <code>
          <span class="keyword">void</span> initialize(<GapWord :correctWord="'Graph'" /> graph, <GapWord :correctWord="'int'" /> startNode, <GapWord :correctWord="'double[]'" /> distance, <GapWord :correctWord="'int[]'" /> predecessor, ArrayList &lt;Integer&gt; notIncluded) {
            <span class="keyword">for</span> (<span class="keyword">int</span> node : graph.<GapWord :correctWord="'nodes'" />()) {
                distance[<GapWord :correctWord="'node'" />] = <span class="variable">Double.POSITIVE_INFINITY</span>;
                predecessor[<GapWord :correctWord="'node'" />] = <span class="number">-1</span>;
            }
            distance[<GapWord :correctWord="'startNode'" />] = <GapWord :correctWord="'0'" />;
            notIncluded.<span class="function">addAll</span>(graph.<GapWord :correctWord="'nodes'" />());
          }
        </code>
        </pre>
  </div>
  <br>
  <br>
  <div style="text-align: left;" class="border-slate-300 border-4 rounded-lg">
    <pre>
        <code>
          <span class="keyword">void</span> distanceUpdate(<span class="type">Graph</span> graph, <span class="type">int</span> smallestDistanceNode, <span class="type">int</span> currentNeighbour, <span class="variable">double</span>[] distance, <span class="variable">int</span>[] predecessor) {
              <span class="variable">double</span> alternativePathDistance = distance[smallestDistanceNode] <GapWord :correctWord="'+'"/> graph.distance(smallestDistanceNode, currentNeighbour);
              <span class="keyword">if</span> (<GapWord :correctWord="'alternativePathDistance'"/> &lt; distance[currentNeighbour]) {
                  distance[currentNeighbour] = <GapWord :correctWord="'alternativePathDistance'"/>;
                  predecessor[<GapWord :correctWord="'currentNeighbour'"/>] = smallestDistanceNode;
              }
          }
        </code>
      </pre>
  </div>
</template>

<script>
export default {
  components: { GapWord },
  data() {
    return {
      name: 'main',
      points: 0,
      color: "white",
      props: {}
    }
  },
  methods: {
    update() {
      if (document.getElementById("luecke1").value === "awesomeness") {
        this.points = 100
        this.color = "lime"
      }
      else {
        this.points = 0
        this.color = "red"
      }
    },
    onChildUpdate(message) {
      this.points += 1
    }
  }
}
</script>

<style scoped>
.input1 {
  color: v-bind(color);
  padding: 3px;
  border-radius: 5px;
  background: #242424;
  background:
    linear-gradient(white, white) center bottom 5px /calc(100% - 10px) 2px no-repeat;
}

/* Java syntax highlighting */
.keyword {
  color: #569CD6;
  font-weight: bold;
}

.type {
  color: #4EC9B0;
}

.string {
  color: #D69D85;
}

.comment {
  color: #6A9955;
  font-style: italic;
}

.variable {
  color: #DCDCAA;
}

.number {
  color: #B5CEA8;
}

div {
  min-width: min-content;
}
</style>
