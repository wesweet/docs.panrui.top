<!--
 * @Description:
 * @Author: panrui
 * @Date: 2023-06-13 08:27:03
 * @LastEditTime: 2023-08-01 08:56:53
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->

- [中文文档](https://www.nextjs.cn/docs/getting-started)

```
npm i -g create-next-app
```

## 基本特性

- 一个页面就是一个从 pages 目录中的 React 组件

#### 静态生成与服务器端渲染

- 静态生成

  > 1. 生成 HTML 时，可以预先渲染好页面，并将其作为“静态”文件（HTML 文件）提供给用户
  > 2. 生成的 HTML 文件可以被 CDN 缓存，以提高性能，并且可以在没有 JavaScript 的情况下运行
  > 3. 生成的 HTML 文件可以被搜索引擎爬取，以改善 SEO

- 服务器端渲染

  > 1. 服务器端渲染（SSR）是在每次请求时生成 HTML
  > 2. 服务器端渲染（SSR）的页面可以使用动态数据

```js
// 静态生成不带数据的静态页面
export default function Home() {
  return <div>hello world</div>;
}

// 静态生成带数据的静态页面
function Home({ posts }) {
  return (
    <ul>
      {posts.map((post) => (
        <li>{post.title}</li>
      ))}
    </ul>
  );
}

export async function getStaticProps() {
  // 调用外部 API 获取博文列表
  const res = await fetch("https://.../posts");
  const posts = await res.json();

  // 通过返回 { props: posts } 对象，Blog 组件
  // 在构建时将接收到 `posts` 参数
  return {
    props: {
      posts,
    },
  };
}

// 静态生成带数据的静态页面，带有动态路由
function Post({ post }) {
  // Render post...
}

// 该函数在构建时被调用
export async function getStaticPaths() {
  // 调用外部 API 获取博文列表
  const res = await fetch("https://.../posts");
  const posts = await res.json();

  // 根据博文列表生成所有需要预渲染的路径
  const paths = posts.map((post) => `/posts/${post.id}`);

  // { fallback: false } 表示其他路由应该 404
  return { paths, fallback: false };
}

// 在构建时也会被调用
export async function getStaticProps({ params }) {
  // params 包含此片博文的 `id`。
  // 如果路由是 /posts/1，那么 params.id 就是 1
  const res = await fetch(`https://.../posts/${params.id}`);
  const post = await res.json();

  // 通过返回 { props: { post } } 对象，Blog
  // 组件在构建时将接收到 `post` 参数
  return {
    props: {
      post,
    },
  };
}

// 服务器端渲染
function Profile({ user }) {
  return <h1>{user.name}</h1>;
}

// 该函数在每个请求时被调用
export async function getServerSideProps(context) {
  // 调用外部 API 获取用户数据
  const res = await fetch(`https://.../user/${context.params.id}`);
  const user = await res.json();

  // 通过返回 { props: { user } } 对象，Profile 组件
  // 在每个请求时将接收到 `user` 参数
  return {
    props: {
      user,
    },
  };
}
```

#### 动态路由


最后更新时间：2024-4-30 09:49:57