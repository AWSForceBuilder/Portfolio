// pages/index.js or pages/index.tsx
import React from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { getBlogPosts, getProjects } from "@/lib/cms";

export default function Home({ blogPosts, projects }) {
  return (
    <div className="container mx-auto p-6">
      <header className="text-center">
        <h1 className="text-4xl font-bold">Welcome to My Portfolio</h1>
        <p className="text-lg mt-2">Salesforce & AWS Professional | CPQ Specialist</p>
      </header>

      <section className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6 mt-8">
        <Card>
          <CardContent>
            <h2 className="text-xl font-semibold">About Me</h2>
            <p>Experienced Salesforce Administrator & AWS Certified Professional.</p>
            <Link href="/about"><Button className="mt-2">Learn More</Button></Link>
          </CardContent>
        </Card>

        <Card>
          <CardContent>
            <h2 className="text-xl font-semibold">Projects</h2>
            <ul>
              {projects.map((project) => (
                <li key={project.id}>{project.title}</li>
              ))}
            </ul>
            <Link href="/projects"><Button className="mt-2">View Projects</Button></Link>
          </CardContent>
        </Card>

        <Card>
          <CardContent>
            <h2 className="text-xl font-semibold">Blog</h2>
            <ul>
              {blogPosts.map((post) => (
                <li key={post.id}>{post.title}</li>
              ))}
            </ul>
            <Link href="/blog"><Button className="mt-2">Visit Blog</Button></Link>
          </CardContent>
        </Card>
      </section>

      <footer className="text-center mt-10">
        <p>&copy; 2024 Your Name. All Rights Reserved.</p>
      </footer>
    </div>
  );
}

// Fetch data at build time
export async function getStaticProps() {
  const blogPosts = await getBlogPosts();
  const projects = await getProjects();
  return {
    props: {
      blogPosts,
      projects,
    },
  };
}
